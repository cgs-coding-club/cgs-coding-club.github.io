---
layout: post
title: Sorting implementations (C++)
---

### Bubble sort

```cpp
for (int i = 0; i < n - 1; i++) {
  for (int j = i; j < n; j++) {
      if (s[i] > s[j]) {
          swap(s[i], s[j]);
      }
  }
}
```

### Insertion sort

```cpp
for (int i = 1; i < n; i++) {
  for (int j = i; j > 0; j--) {
    if (s[j] < s[j - 1]) {
      swap(s[j - 1], s[j]);
    } else {
      break;
    }
  }
}
```

### Selection sort

```cpp
for (int i = n - 1; i >= 0; i--) {
  for (int j = 0; j < i; j++) {
    if (s[i] < s[j]) swap(s[i], s[j]);
  }
}
```

### Quicksort (pivoting)

```cpp
vector<int> merge_vectors(vector<int> a, vector<int> b, vector<int> c) {
  vector<int> res;

  for (auto el : a) {
    res.push_back(el);
  }
  for (auto el : b) {
    res.push_back(el);
  }
  for (auto el : c) {
    res.push_back(el);
  }

  return res;
}


vector<int> qsort(vector<int> s) {
  if (s.size() <= 1) {
    return s;
  }
  uniform_int_distribution<> dst(0, s.size() - 1);
  int pivot_index = dst(gen);

  vector<int> left;
  vector<int> right;
  vector<int> middle;

  int n = s.size();

  for (int i = 0; i < n; i++) {
    if (s[i] < s[pivot_index]) {
      left.push_back(s[i]);
    } else if (s[i] == s[pivot_index]) {
      middle.push_back(s[i]);
    } else {
      right.push_back(s[i]);
    }
  }

  return merge_vectors(qsort(left), middle, qsort(right));
}
```

### Merge sort (didn't discuss, but still posting it here)

```cpp
vector<ll> merge(vector<ll> a, vector<ll> b) {
  vector<ll> result;
  while (!a.empty() || !b.empty()) {
    if (b.empty()) {
      result.push_back(a.back());
      a.pop_back();
    } else if (a.empty()) {
      result.push_back(b.back());
      b.pop_back();
    } else {
      if (a.back() < b.back()) {
        result.push_back(b.back());
        b.pop_back();
      } else {
        result.push_back(a.back());
        a.pop_back();
      }
    }
  }
  reverse(result.begin(), result.end());
  return result;
}

vector<ll> merge_sort(vector<ll> s) {
  if (s.size() <= 1) {
    return s;
  }

  vector<ll> s1;
  vector<ll> s2;

  for (ll i = 0; i < s.size() / 2; i++) {
    s1.push_back(s[i]);
  }


  for (ll i = s.size() / 2; i < s.size(); i++) {
    s2.push_back(s[i]);
  }

  return merge(merge_sort(s1), merge_sort(s2));
}
```