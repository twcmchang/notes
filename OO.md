Python is a multiparadigm programming language, which allows us to adopt procedural, object-oriented, functional ... styles.

# Self-defined class
```
import math
class Point:
  def __init__(self,x,y):
    self.x = x
    self.y = y
  def distance_from_origin(self):
    return math.sqrt((x**2)+(y**2))
  def __eq__(self,other):
    return self.x == other.x and self.y == other.y
  def __repr__(self):
    return "Point({0.x!r},{0.y!r})".format(self)
  def __str__(self):
    return "({0.x!r},{0.y!r})".format(self)
```
