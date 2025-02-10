# editor-diff-track

A lightweight wrapper around [`diff-match-patch`](https://github.com/google/diff-match-patch), providing enhanced functionality for tracking text differences in editors.

[![NPM version](https://img.shields.io/npm/v/editor-diff-track.svg)](https://www.npmjs.com/package/editor-diff-track)
[![License](https://img.shields.io/github/license/Rohit-R-Sahu/editor-diff-track.svg)](./LICENSE)
[![GitHub Issues](https://img.shields.io/github/issues/Rohit-R-Sahu/editor-diff-track.svg)](https://github.com/Rohit-R-Sahu/editor-diff-track/issues)

## Installation

```sh
npm install editor-diff-track
```

## Overview

This package provides a simple API for computing and formatting text differences. It is based on Google's [`diff-match-patch`](https://github.com/google/diff-match-patch) but offers a cleaner integration for modern JavaScript/TypeScript projects.

## API

### Importing the Library

```javascript
import DiffMatchPatch from 'editor-diff-track';

const dmp = new DiffMatchPatch();
const diff = dmp.diff_main('dogs bark', 'cats bark');
console.log(diff);
```

### Methods

#### `diff_main(text1, text2) → diffs`
Computes an array of differences describing the transformation of `text1` into `text2`.

```javascript
dmp.diff_main("Good dog", "Bad dog"); 
// Output: [(-1, "Goo"), (1, "Ba"), (0, "d dog")]
```

#### `diff_cleanupSemantic(diffs) → null`
Cleans up a diff by merging adjacent small differences into more meaningful changes.

```javascript
const diffs = dmp.diff_main("mouse", "sofas");
dmp.diff_cleanupSemantic(diffs);
console.log(diffs);  
// Output: [(-1, "mouse"), (1, "sofas")]
```

#### `diff_cleanupEfficiency(diffs) → null`
Optimizes a diff for efficient machine processing.

```javascript
dmp.diff_cleanupEfficiency(diffs);
console.log(diffs);
```

#### `diff_levenshtein(diffs) → int`
Computes the Levenshtein distance (edit distance) between two texts based on a diff.

```javascript
const distance = dmp.diff_levenshtein(diff);
console.log(distance);
```

#### `diff_prettyHtml(diffs) → html`
Formats a diff as an HTML representation.

```javascript
const htmlDiff = dmp.diff_prettyHtml(diff);
console.log(htmlDiff);
```

#### `patch_make(text1, text2) → patches`
Generates a list of patch objects representing the changes needed to transform `text1` into `text2`.

```javascript
const patches = dmp.patch_make("hello world", "hello new world");
console.log(patches);
```

#### `patch_apply(patches, text1) → [text2, results]`
Applies a list of patches to `text1`.

```javascript
const [newText, results] = dmp.patch_apply(patches, "hello world");
console.log(newText, results);
```

## Usage Example

```javascript
import DiffMatchPatch from 'editor-diff-track';

const dmp = new DiffMatchPatch();
const text1 = "The quick brown fox";
const text2 = "The quick blue fox";

const diffs = dmp.diff_main(text1, text2);
dmp.diff_cleanupSemantic(diffs);

console.log(diffs);
// Output: [(0, "The quick "), (-1, "brown"), (1, "blue"), (0, " fox")]
```

## License

This project is licensed under the **MIT License**.

However, it is based on the [`diff-match-patch`](https://github.com/google/diff-match-patch) project, which is originally licensed under **Apache 2.0**.

For more details, see:
- [`LICENSE`](./LICENSE) (MIT License)
- [`LICENSE-APACHE`](./LICENSE-APACHE) (Original Apache 2.0 License)

### GitHub Repository: [Rohit-R-Sahu/editor-diff-track](https://github.com/Rohit-R-Sahu/editor-diff-track)


**Modifications:**  
This package serves as a wrapper around `diff-match-patch` with enhancements for easier integration in JavaScript projects.