# iter_arff

Iterates over rows from an ARFF file.



## Parameters

- **filepath_or_buffer**

    Either a string indicating the location of a CSV file, or a buffer object that has a `read` method.

- **target** (*str*) – defaults to `None`

    Name of the target field.

- **compression** – defaults to `infer`

    For on-the-fly decompression of on-disk data. If this is set to 'infer' and `filepath_or_buffer` is a path, then the decompression method is inferred for the following extensions: '.gz', '.zip'.




