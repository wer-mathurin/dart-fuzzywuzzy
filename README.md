# FuzzyWuzzy

[![Tests](https://github.com/SphericalKat/dart-fuzzywuzzy/actions/workflows/test.yml/badge.svg)](https://github.com/SphericalKat/dart-fuzzywuzzy/actions/workflows/test.yml)
![Coverage](https://raw.githubusercontent.com/sphericalkat/dart-fuzzywuzzy/master/coverage_badge.svg?sanitize=true)

This is a dart port of the popular [FuzzyWuzzy](https://github.com/seatgeek/fuzzywuzzy) python package. This algorithm uses [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) to calculate similarity between strings.

I personally needed to use this for my own search algorithms, and there weren't any packages as good as my experience with FuzzyWuzzy was, so here we are. Enjoy!

- No dependencies.
- Pure Dart implementation of the superfast [python-Levenshtein](https://github.com/ztane/python-Levenshtein/).
- Simple to use.
- Lightweight.
- Massive props to the folks over at seatgeek for coming up with the [algorithm](https://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/).

## Get started

### Add dependency

```yaml
dependencies:
  fuzzywuzzy: 0.1.3 # latest version
```

## Usage

First, import the package

```dart
import 'package:fuzzywuzzy/fuzzywuzzy.dart'
```

### Simple ratio

```dart
ratio("mysmilarstring", "myawfullysimilarstirng") // 72
ratio("mysmilarstring", "mysimilarstring")        // 97
```

### Partial ratio

```dart
partialRatio("similar", "somewhresimlrbetweenthisstring") // 71
```

### Token sort ratio

```dart
tokenSortPartialRatio("order words out of", "words out of order") // 100
tokenSortRatio("order words out of","  words out of order")       // 100
```

### Token set ratio

```dart
tokenSetRatio("fuzzy was a bear", "fuzzy fuzzy fuzzy bear")         // 100
tokenSetPartialRatio("fuzzy was a bear", "fuzzy fuzzy fuzzy bear")  // 100
```

### Weighted ratio

```dart
weightedRatio("The quick brown fox jimps ofver the small lazy dog", "the quick brown fox jumps over the small lazy dog") // 97
```

### Extract

```dart
extractOne(
        query: 'cowboys',
        choices: [
          'Atlanta Falcons',
          'New York Jets',
          'New York Giants',
          'Dallas Cowboys'
        ],
        cutoff: 10,
      ) // (string Dallas Cowboys, score: 90, index: 3)
```

```dart
extractTop(
        query: 'goolge',
        choices: [
          'google',
          'bing',
          'facebook',
          'linkedin',
          'twitter',
          'googleplus',
          'bingnews',
          'plexoogl'
        ],
        limit: 4,
        cutoff: 50,
      ) // [(string google, score: 83, index: 0), (string googleplus, score: 75, index: 5)]
```
```dart
extractAllSorted(
        query: 'goolge',
        choices: [
          'google',
          'bing',
          'facebook',
          'linkedin',
          'twitter',
          'googleplus',
          'bingnews',
          'plexoogl'
        ],
        cutoff: 10,
      ) // [(string google, score: 83, index: 0), (string googleplus, score: 75, index: 5), (string plexoogl, score: 43, index: 7), (string bingnews, score: 29, index: 6), (string linkedin, score: 29, index: 3), (string facebook, score: 29, index: 2), (string bing, score: 23, index: 1), (string twitter, score: 15, index: 4)]
```
```dart
extractAll(
        query: 'goolge',
        choices: [
          'google',
          'bing',
          'facebook',
          'linkedin',
          'twitter',
          'googleplus',
          'bingnews',
          'plexoogl'
        ],
        cutoff: 10,
      ) // [(string google, score: 83, index: 0), (string bing, score: 23, index: 1), (string facebook, score: 29, index: 2), (string linkedin, score: 29, index: 3), (string twitter, score: 15, index: 4), (string googleplus, score: 75, index: 5), (string bingnews, score: 29, index: 6), (string plexoogl, score: 43, index: 7)]
```
