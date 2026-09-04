Credit: This action is adapted from: https://github.com/dkershner6/switch-case-action, since that project is no longer maintained.

To date, the only change we've made is to use a different regex action to resolve a `set-output` deprecation warning that occurred in the aforementioned project.

# switch-case-action

Easily return one of many values based on many conditionals.

## conditionals-with-values

New lines are required between conditionals, what needs to occur for this switch case to work is for the word "true" to occur, then any amount of white space (or none) an arrow (=>) then any amount of whitespace. It will return all remaining text on that line.

## Usage

```yml
      - uses: everfend/switch-case-action@v1
        id: switch-case
        with:
          default: "its the default"
          conditionals-with-values: |
            ${{ 'test' == 'not-test' }} => shouldnt be this one
            ${{ 'test' == 'test' }} => correctAnswer
          
      - run: echo ${{ steps.switch-case.outputs.value }} # correctAnswer
```


```yml
      - uses: everfend/switch-case-action@v1
        id: switch-case
        with:
          default: "its the default"
          conditionals-with-values: |
            ${{ 'test' == 'not-test' }} => shouldnt be this one
            ${{ 'test' == 'still-not-test' }} => shouldnt be this one, too
          
      - run: echo ${{ steps.switch-case.outputs.value }} # its the default
```
