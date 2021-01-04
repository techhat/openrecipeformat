{
  "$schema": "http://json-schema.org/draft-07/schema",
  "definitions": {
    "none": {
      "type": "string",
      "enum": [
        "none",
        "None"
      ]
    },
    "note": {
      "type": "string"
    },
    "unit": {
      "type": "string",
      "title": "Unit",
      "examples": [
        "cups",
        "tsp",
        "g",
        "kg",
        "l",
        "dl",
        "cl",
        "each"
      ]
    },
    "usda_num": {
      "anyOf": [
        {
          "type": "integer"
        },
        {
          "type": "string",
          "pattern": "^[0-9]+$"
        }
      ],
      "description": "This corresponds with the index keys in the USDA Standard Reference. It is generally used for easy lookup of nutritional data. If possible, this should be used, and USDA data, when available, is preferable to any other nutritional data source."
    },
    "step": {
      "type": "object",
      "properties": {
        "step": {
          "type": "string",
          "description": "Description of the step."
        },
        "notes": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/note"
          },
          "description": "A list of notes relevant to this step. Often known as “bench notes” to professionals."
        },
        "haccp": {
          "type": "object",
          "properties": {
            "control_point": {
              "type": "string",
              "description": "Refers to specific HACCP guidelines relevant to this step."
            },
            "critical_control_point": {
              "type": "string",
              "description": "Refers to specific HACCP guidelines relevant to this step, which are critical to the safety outcome of this recipe."
            }
          },
          "description": "Can contain either a control_point or a critical_control_point. Should not contain both.",
          "minProperties": 1,
          "maxProperties": 1
        }
      },
      "required": [
        "step"
      ],
      "additionalProperties": false,
      "description": "Describes step to be performed on the recipe."
    },
    "ingredient": {
      "type": "object",
      "patternProperties": {
        "^[a-zA-Z ]*$": {
          "type": "object",
          "properties": {
            "amounts": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "amount": {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "string"
                      }
                    ],
                    "description": "The amount of the unit to use."
                  },
                  "unit": {
                    "$ref": "#/definitions/unit",
                    "description": "The unit, relevant to the amount."
                  }
                },
                "required": [
                  "amount",
                  "unit"
                ],
                "additionalProperties": false
              },
              "description": "A list of dicts which describe the amounts to use. Normally, the list will only contain one dict. In cases where multiple yields need to be stored (i.e. 50 cookies vs 100 cookes vs 250 cookies), each yield will have its own dict in this list, in the same order as the recipe’s yield field."
            },
            "processing": {
              "type": "array",
              "items": {
                "type": "string"
              },
              "description": "A list of tags which describe the processing of this item. For instance, “whole”, “large dice”, “minced”, “raw”, “steamed”, etc.",
              "examples": [
                "whole",
                "diced",
                "minced",
                "steamed",
                "raw"
              ]
            },
            "notes": {
              "type": "array",
              "items": {
                "$ref": "#/definitions/note"
              },
              "description": "Any notes specific to this ingredient"
            },
            "substitutions": {
              "type": "array",
              "items": {
                "$ref": "#/definitions/ingredient"
              },
              "description": "This field is a list of ingredients, in exactly the same format as a regular ingredient list item, minus the substitutions field."
            },
            "usda_num": {
              "$ref": "#/definitions/usda_num",
              "description": "This corresponds with the index keys in the USDA Standard Reference. It is generally used for easy lookup of nutritional data. If possible, this should be used, and USDA data, when available, is preferable to any other nutritional data source."
            }
          },
          "required": [
            "amounts"
          ],
          "additionalProperties": false
        }
      },
      "minProperties": 1,
      "maxProperties": 1
    }
  },
  "type": "object",
  "properties": {
    "recipe_name": {
      "type": "string",
      "description": "The name of this recipe."
    },
    "notes": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/note"
      },
      "description": "General notes about the recipe."
    },
    "steps": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/step"
      },
      "description": "A list, in order, of steps to be performed on the recipe."
    },
    "ingredients": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/ingredient"
      },
      "description": "A list of dicts, defining which food items are to be added to the recipe. These items should be listed in the order in which they are to be used. Bearing this in mind, a particular item may be listed multiple times, if it is to be used multiple times and/or at different quantities in a recipe."
    },
    "oven_fan": {
      "oneOf": [
        {
          "$ref": "#/definitions/none"
        },
        {
          "type": "string",
          "enum": [
            "Off",
            "Low",
            "High"
          ]
        }
      ],
      "description": "Setting to be used with convection oven. Possible values are “Off”, “Low” and “High”. If not specified, it is assumed to be “Off”. If specified, all software should display and print this value. If not specified, it is up to the software whether or not it is displayed and/or printed, but it should be consistent."
    },
    "oven_temp": {
      "oneOf": [
        {
          "$ref": "#/definitions/none"
        },
        {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "amount": {
                "type": "number"
              },
              "unit": {
                "type": "string",
                "enum": [
                  "C",
                  "F"
                ]
              }
            },
            "minProperties": 2,
            "maxProperties": 2
          }
        }
      ],
      "description": "Starting oven temperature, if the oven is used."
    },
    "oven_time": {
      "description": "How long the dish should spend in the oven. This is an overall value, which refers to the recipe as a whole. If multiple oven times are used, they should be specified in the recipe."
    },
    "recipe_uuid": {},
    "source_book": {
      "oneOf": [
        {
          "type": "object",
          "properties": {
            "authors": {
              "type": "array",
              "items": {
                "type": "string"
              },
              "description": "This is a list. Refers to the author(s) of this recipe. Can be the same as source_authors, if appropriate. If there was only one author, then they would be the only item in the list."
            },
            "title": {
              "type": "string",
              "description": "Title of the book. This is a single value, not a list."
            },
            "isbn": {
              "type": "string",
              "description": "International Standard Book Number, if available."
            },
            "notes": {
              "type": "array",
              "items": {
                "$ref": "#/definitions/note"
              },
              "description": "Any information about the book that does not fit into another field."
            }
          },
          "patternProperties": {
            "^X-.*$": {
              "description": "A lot of different information about a book can be stored. Until a field has been officially accepted into the spec, it should start with a capital X, followed by a dash."
            }
          },
          "additionalProperties": false,
          "required": [
            "title",
            "authors"
          ]
        },
        {
          "$ref": "#/definitions/none"
        }
      ],
      "description": "If this recipe was originally pulled from a book, then the book information should go here. Recipe software should make an intelligent effort to include correct information in the correct fields, rather than just dumping everything into a generic notes field."
    },
    "source_authors": {
      "oneOf": [
        {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        {
          "type": "string"
        }
      ],
      "description": "Does not refer to the person who entered the recipe; only refers to the original author of the recipe. If this recipe was based on another recipe by another person, then this field should contain the name of the original author."
    },
    "source_url": {
      "type": "string",
      "description": "The URL that this recipe was copied from, if applicable. In the case of a recipe-hosting website, this may refer to the official URL at which the recipe is hosted."
    },
    "yields": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "amount": {
            "type": "number"
          },
          "unit": {
            "$ref": "#/definitions/unit"
          }
        },
        "dependencies": {
          "amount": {
            "required": [
              "unit"
            ]
          }
        },
        "additionalProperties": {
          "type": "number"
        },
        "maxProperties": 2
      },
      "description": "Refers to how much food the recipe makes. This is a list, which will normally contain one dict. In cases where multiple yields need to be stored (i.e. 50 cookies vs 100 cookes vs 250 cookies), each yield will have its own dict in this list."
    },
    "author": {
      "type": "string"
    },
    "nutrition": {
      "type": "object",
      "patternProperties": {
        "^[a-zA-Z ]*$": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "unit": {
                "$ref": "#/definitions/unit"
              },
              "amount": {
                "type": "number"
              },
              "usda_name": {
                "type": "string"
              },
              "usda_num": {
                "$ref": "#/definitions/usda_num"
              },
              "proximates": {
                "type": "object",
                "properties": {
                  "water": {
                    "type": "number"
                  },
                  "energy": {
                    "type": "number"
                  },
                  "protein": {
                    "type": "number"
                  },
                  "lipid_total": {
                    "type": "number"
                  },
                  "ash": {
                    "type": "number"
                  },
                  "carbohydrate": {
                    "type": "number"
                  },
                  "fiber_total": {
                    "type": "number"
                  },
                  "sugars_total": {
                    "type": "number"
                  },
                  "sucrose": {
                    "type": "number"
                  },
                  "glucose": {
                    "type": "number"
                  },
                  "fructose": {
                    "type": "number"
                  },
                  "lactose": {
                    "type": "number"
                  },
                  "maltose": {
                    "type": "number"
                  },
                  "galactose": {
                    "type": "number"
                  },
                  "starch": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              },
              "minerals": {
                "type": "object",
                "properties": {
                  "calcium": {
                    "type": "number"
                  },
                  "iron": {
                    "type": "number"
                  },
                  "magnesium": {
                    "type": "number"
                  },
                  "phosphorus": {
                    "type": "number"
                  },
                  "potassium": {
                    "type": "number"
                  },
                  "sodium": {
                    "type": "number"
                  },
                  "zinc": {
                    "type": "number"
                  },
                  "copper": {
                    "type": "number"
                  },
                  "manganese": {
                    "type": "number"
                  },
                  "selenium": {
                    "type": "number"
                  },
                  "flouride": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              },
              "vitamins": {
                "type": "object",
                "properties": {
                  "vitamin_c": {
                    "type": "number"
                  },
                  "thiamin": {
                    "type": "number"
                  },
                  "riboflavin": {
                    "type": "number"
                  },
                  "niacin": {
                    "type": "number"
                  },
                  "pantothenic_acid": {
                    "type": "number"
                  },
                  "vitamin_b6": {
                    "type": "number"
                  },
                  "folate_total": {
                    "type": "number"
                  },
                  "folic_acid": {
                    "type": "number"
                  },
                  "folate_food": {
                    "type": "number"
                  },
                  "folate_dfe": {
                    "type": "number"
                  },
                  "choline_total": {
                    "type": "number"
                  },
                  "betaine": {
                    "type": "number"
                  },
                  "vitamin_b12": {
                    "type": "number"
                  },
                  "vitamin_b12_added": {
                    "type": "number"
                  },
                  "vitamin_a_rae": {
                    "type": "number"
                  },
                  "retinol": {
                    "type": "number"
                  },
                  "carotene_beta": {
                    "type": "number"
                  },
                  "carotene_alpha": {
                    "type": "number"
                  },
                  "cryptoxanthin_beta": {
                    "type": "number"
                  },
                  "vitamin_a_iu": {
                    "type": "number"
                  },
                  "lycopene": {
                    "type": "number"
                  },
                  "lutein_zeaxanthin": {
                    "type": "number"
                  },
                  "vitamin_e_alpha_tocopherol": {
                    "type": "number"
                  },
                  "vitamin_e_added": {
                    "type": "number"
                  },
                  "vitamin_e": {
                    "type": "number"
                  },
                  "tocopherol_beta": {
                    "type": "number"
                  },
                  "tocopherol_gamma": {
                    "type": "number"
                  },
                  "tocopherol_delta": {
                    "type": "number"
                  },
                  "vitamin_d2_d3": {
                    "type": "number"
                  },
                  "vitamin_d_ergocalciferol": {
                    "type": "number"
                  },
                  "vitamin_d_cholecalciferol": {
                    "type": "number"
                  },
                  "vitamin_d": {
                    "type": "number"
                  },
                  "vitamin_k": {
                    "type": "number"
                  },
                  "menaquinone_4": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              },
              "lipids": {
                "type": "object",
                "properties": {
                  "total_saturated": {
                    "type": "number"
                  },
                  "total_monounsaturated": {
                    "type": "number"
                  },
                  "total_polyunsaturated": {
                    "type": "number"
                  },
                  "cholesterol": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              },
              "other": {
                "type": "object",
                "properties": {
                  "caffeine": {
                    "type": "number"
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "patternProperties": {
    "^X-[a-zA-z]+$": {
      "description": "A lot of different information about a recipe can be stored. Until a field has been officially accepted into the spec, it should start with a capital X, followed by a dash."
    }
  },
  "required": [
    "recipe_name",
    "steps",
    "ingredients"
  ],
  "additionalProperties": false
}
