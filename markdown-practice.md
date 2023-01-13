# Markdown Practice

> This page serves to demonstrate the many different ways in which markdown can be utilized.

---

## Here are some of my favorite things:

A show that I'm watching right now: [Suits](https://www.amazon.com/Suits-Season-1/dp/B005544TRQ)

Some great songs:
* Fly Me to the Moon - Frank Sinatra
* All of Me - John Legend
* Blinding Lights - The Weeknd

Top 3 Avengers Movies:
1) Iron Man
2) Black Panther
3) Doctor Strange

The most overrated piece of code: 'print("Hello World")' or any variation of that in any language

Code that I like:
'''
binarySearch(array, target, start, end) {
  if (start > end) {
    return -1;
  }
  mid = (start + end) / 2
  if (array[mid] == target) {
    return mid;
  }
  else if (array[mid] < target) {
    return binarySearch(array, target, mid + 1, end)
  }
  else if (array[mid] > target) {
    return binarySearch(array, target, start, mid - 1)
  }
}
'''

