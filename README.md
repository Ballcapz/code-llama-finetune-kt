# code-llama-finetune-kt

Finetuning Code Llama on my own kotlin codebase.

- Used [this](https://github.com/samlhuillier/code-llama-fine-tune-notebook) notebook as an outline to train the model.
- Used [RunPod](runpod.io) to perform the training.


# Constructing the dataset

I wanted to extract only functions from my Kotlin codebase. I used the [Python Tree Sitter](https://github.com/tree-sitter/py-tree-sitter)
and [kotlin-tree-sitter](https://github.com/fwcd/tree-sitter-kotlin) to parse all of my files and generate an AST. Then I found all function definitions and collected them until I had the entire set of functions
in the codebase. Finally, I naively tokenized each function to build out a training and eval dataset using only the code I had parsed.

The training data was formatted as such:
```jsonl
{"input": "fun myFunction(", "output": "\n    arg1: String,\n): String {\n    return arg1\n}"}
```
Representing this function:
```kt
fun myFunction(
    arg1: String
): String {
    return arg1
}
```

And had many combinations of that function.


# Conclusions
- I haven't done enough testing to make any real conclusions, but upon initial checking of the model, I believe I have overtrained it on the specific code
in my code base. I think I added to many input/output pairs that are effectively the same.
- Next Training Iteration: I will construct the dataset more sparsely, as well as use comments and/or generated text queries as inputs to match similar outputs




