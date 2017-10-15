Python is a multiparadigm programming language, which allows us to adopt procedural, object-oriented, functional ... styles.

# Self-defined class
```
import math
class Point:
  def __init__(self,x,y):
    super().__init__()              # call super class __init__ first
    self.x = x
    self.y = y
    
  def distance_from_origin(self):
    return math.sqrt((x**2)+(y**2))
    
  def __eq__(self,other):           # no need to implement __ne__() (!=)
    # (1) assert isinstance(other,Point)
    # (2) if not isinstance(other,Point):
    #        raise TypeError
    # (3) if not isinstance(other,Point):
    #        return NotImplement    # => will find other.__eq__() to check if any other method to meet Point
    return self.x == other.x and self.y == other.y
    
  def __repr__(self):               # return a string or the result after eval()
    return "Point({0.x!r},{0.y!r})".format(self)
    
  def __str__(self):
    return "({0.x!r},{0.y!r})".format(self)
```
