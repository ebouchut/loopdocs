<!-- Regular Markdown Page importing a section of a shared page  -->

Once the {{ app }} application is installed we need to _configure_ it.

## Configuration

{%
    include-markdown "../shared/app.md"
    start="<!--config-start-->"
    end="<!--config-end-->"
%}

Once the {{ app}} application is configured, we can use it like so...

## Usage

{%
    include-markdown "../shared/app.md"
    start="<!--usage-start-->"
    end="<!--usage-end-->"
%}

## Debug

{{ macros_info() }}
