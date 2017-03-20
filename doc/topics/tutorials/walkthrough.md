# Getting Started

The Open Recipe Format was designed to be as simple as possible for basic applications, while also being flexible enough to handle various complexities that may be encountered in production environments. This guide outlines the basic file format, what needs to be defined at a bare minimum, and how to put it all together.

At its heart, the Open Recipe Format (ORF) uses an established file format called YAML. It's not a difficult format to get used to, but using a syntax checker will save you from a lot of headaches. An excellent online resource can be found at http://yaml-online-parser.appspot.com/.

At its most basic level, a recipe consists of a name, a list of ingredients, and a list of steps to put those ingredients together. At this point, the most complex of these is the ingredient list. Each item in the list consists of an amount, a unit (which is often implied, in traditional recipes), and a corresponding ingredient.

Let's put together a very basic recipe for giving an apple to a friend. In a non-computer parsable format, we might say, "Give an apple to a friend." To make this easier for the computer to use, we need to be more specific:

``` sourceCode
recipe_name: Giving an Apple to a Friend
ingredients:
    - apple:
        amounts:
            - amount: 1
              unit: each
steps:
    - step: Give an apple to a friend.
```

This is as basic as a recipe gets. Because we are striving to be specific, there is nothing implied in this recipe; if we were writing it out traditionally, we would say 1 each apple instead of 1 apple. This may feel awkward to some, and developers may choose to allow their users to say 1 apple in their software, but when they save it to an ORF file, it needs to be more specific.

Let's expand this recipe, to include more fruit, and more steps for handling the fruit. This recipe is for a very basic fruit salad, which is unlikely to win any awards, but will still feed your friends.

``` sourceCode
recipe_name: Basic Fruit Salad
yields:
    - servings: 6
ingredients:
    - apple:
        amounts:
            - amount: 1
              unit: each
    - banana:
        amounts:
            - amount: 1
              unit: each
    - orange:
        amounts:
            - amount: 1
              unit: each
    - grapes:
        amounts:
            - amount: 1
              unit: cup
steps:
    - step: Cut the apple into cubes.
    - step: Cut the banana into slices.
    - step: Peel the orange, and divide into segments.
    - step: Combine all ingredients in a bowl.
    - step: Mix to combine.
```

This recipe is fine for 6 people, but what if you need to feed 18 people? An important consideration that most recipe software handles is scaling recipes. However, many commercial environments require multiple scalings to be available in a tidy, concise format. In our case, we would make the following changes to our recipe to handle both at the same time:

``` sourceCode
recipe_name: Basic Fruit Salad
yields:
    - servings: 6
    - servings: 18
ingredients:
    - apple:
        amounts:
            - amount: 1
              unit: each
            - amount: 3
              unit: each
    - banana:
        amounts:
            - amount: 1
              unit: each
            - amount: 3
              unit: each
    - orange:
        amounts:
            - amount: 1
              unit: each
            - amount: 3
              unit: each
    - grapes:
        amounts:
            - amount: 1
              unit: cup
            - amount: 3
              unit: cup
```

A classic use case for this scenario is a bakery, which may need to bake batches of 50, 100, 250, or even more cookies at a time, depending on the occassion. Unfortunately, ingredients are the product of nature, and not all recipes scale as nicely as we would like. It may be that in the case of our bakery, 50 cookies call for 1/2 tablespoon of baking soda, but 250 cookies only calls for 2 tablespoons. It is up to the baker to discover this, but when they do, it will be aggrivating to them to not be able to make note of that in their software.

Speaking of notes, many professional cooks and bakers like to make bench notes when experimenting with recipes. These items of information do not necessarily fit into the classic "steps" format. Fortunately, ORF allows for "notes" to be saved, both alongside specific steps, and outside of the steps. Let's go back to our first recipe, and add some notes.

``` sourceCode
recipe_name: Giving an Apple to a Friend
ingredients:
    - apple:
        amounts:
            - amount: 1
              unit: each
        notes:
            - Use whole apples
            - Pears may be substituted, but produce a different flavor and mouthfeel
steps:
    - step: Give an apple to a friend.
      notes:
        - You can also give an apple to an enemy.
notes:
    - This is a friendly recipe; giving, rather than throwing, is recommended.
```

This recipe contains notes for individual ingredients and steps, as well as for the recipe as a whole. While it is not expected that most cooks, even in the professional kitchen, will take advantage of this, it is fully expected that food scientists will have the opportunity to do so.

Food scientists have a whole new set of information that they need to manage. Precision is key for these individuals, and ORF is designed to handle features that are key to their job success. Consider the following:

``` sourceCode
ingredients:
    - apple:
        usda_num: 09003
        amounts:
            - amount: 1
              unit: each
        processing:
            - whole
            - raw
        substitutions:
            - pears:
                usda_num: 09252
                amounts:
                    - amount: 1
                      unit: each
        notes:
            - Use whole apples
            - Pears may be substituted, but produce a different flavor and mouthfeel
steps:
    - step:
          Gather the apples.
      haccp:
          control_point: The apples must be clean
      notes:
          - Some people like green
          - Some people like red
    - step:
          Hand out the apples.
      haccp:
          critical_control_point: Wash hands with soap and warm water before distributing.
```

This set of ingredients and steps includes a scary amount of detail, for the average layperson. However, it paves the way for the industrialization and safety of this recipe, allowing the user to specify keywords related to processing, and HACCP (Hazard Analysis Critical Control Points)&lt;/topics/tutorials/haccp&gt; instructions to be declared. References to the USDA Standard Reference&lt;/topics/tutorials/usda&gt; are also included, allowing the recipe to make use of nutritional data provided by the USDA.

Now that you have been through a brief overview of the format and its capabilities, the other tutorials and references will make much more sense.
