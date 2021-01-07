Validating ORF Recipe
=====================

The Open Recipe Format is, like other formats, a well-structured format that is
capable of being parsed by machines. To help with ensuring that a recipe follows
the :ref:`orf`, the project includes a JSON schema file. You can read more about
what JSON Schema is `here <https://json-schema.org/>`_, but the gist of it is
that gist of it is a highly structured file that can be used by tools to
automatically validate your recipes.

The schema for ORF can be found within our GitHub repository in the
`./schema.json <https://github.com/techhat/openrecipeformat/blob/master/schema.json>`_
file. After you have downloaded that file to your machine, you may then use it
to validate against your recipe using an external tool like
`ajv <https://ajv.js.org/>`_ or a library like
`python-jsonchema <https://python-jsonschema.readthedocs.io/en/stable/>`_. For
example, to use ajv, after installing it via NPM, you could simply run:

.. code-block:: bash

    ajv validate -s /path/to/schema.json -d /path/to/recipe.yaml

And it will then print out whether the YAML file follows the ORF reference, or
if there are errors in it. The ORF project currently does not provide any
explicit validation software, nor provides any recommendation beyond the ones
above.

Finally, this schema can then be hooked up to various IDEs and text editors
to provide feeedback as you work. For example, if you use
`VSCode <https://code.visualstudio.com/>`_, then you can use the
`YAML <https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml>`_
extension, registering our schema manually with the service, and then get
inline intellisense as you work.
