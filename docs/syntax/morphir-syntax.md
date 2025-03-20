# Morphir Syntax

Unlike other programming languages Morphir does not come with its own syntax. We think that there are enough programming languages out there already so we didn't want to invent a completely new one. Instead Morphir allows you to define your domain model and write your business logic using existing languages but provides tooling to compile all that into the Morphir IR.

While the Morphir IR is a JSON format it designed for efficient programmatic access so it is rather difficult to digest for a human being. In certain situations though, you do want to directly interact with the Morphir IR without the need to go through an intermediary language. In these situations it would be handy to have a dedicated Morphir syntax.

In this document we will define such a syntax but to stick to the original plan we won't do it in the traditional way of coming up with a whole new text syntax that needs its own parser. Instead we will define a JSON format that is simple enough to be authored by a human, but still doesn't require a parser.

morphir-package.json

## Modules

```json
{
    "module": "Trade",
    "docs": "This module defines the key concepts and entities involved in trading operations, such as accounts, securities, trade orders, and their states. It captures the essential details needed to represent and process trades, including trade directions, quantities, and outcomes.",
    "types": {
        "TradeState": {
            "oneOf": ["New", "Processing", "Settled", "Cancelled"]
        },
        "Account": {
            "recordOf": {
                "id": "integer",
                "displayName": "string"
            }
        },
        "Security": {
            "recordOf": {
                "ticker": "string",
                "companyName": "string"
            }
        },
        "TradeSide": {
            "oneOf": ["Buy", "Sell"]
        },
        "TradeOrder": {
            "recordOf": {
                "id": "string",
                "state": "string",
                "security": "string",
                "quantity": "integer",
                "accountId": "integer",
                "side": "TradeSide"
            }
        },
        "TradeRequest": {
            "recordOf": {
                "accountId": "integer",
                "security": "string",
                "side": "TradeSide",
                "quantity": "integer"
            }
        },
        "TradeResponse": {
            "recordOf": {
                "success": "boolean",
                "id": "string",
                "errorMessage": "string"
            }
        }
    },
    "mappings": [
        {
            "from": "TradeState",
            "to": "string",
            "mapping": {
                "New": "N",
                "Processing": "P", 
                "Settled": "S", 
                "Cancelled": "C"
            }
        }
    ],
    "values": {
        "isCompletedState": {
            "function": {
                "inputs": {
                    "tradeState": "TradeState"
                },
                "output": "boolean",
                "logic": {
                    ":member": {
                        "subject": {"input": "tradeState"},
                        "of": ["Settled", "Cancelled"]
                    }
                } 
            }
        }
    }
}
```