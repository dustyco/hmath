Linear Algebra
==============
Dimension and type generic vector and matrix template types plus useful operators and functions.
Include the `hmath` namespace and typedef the templates you want for convenience. 

	#include <iostream>
	using namespace std;
	
	#include "linear_algebra.h"
	using namespace hmath;
	typedef vec<3,float> Vec;
	
	int main ()
	{
		Vec v(1.2, 3.4, 5.6);
		
		cout << v << endl;
	}

Output:

	(1.2, 3.4, 5.6)


Linear Algebra: Operators and Functions
---------------------------------------
`R` -- Scalar template parameter type.  All operators and functions work for any template size and type unless otherwise stated.

Operators:

* `vec (+, -, +=, -=) vec` -- Adds cooresponding components
* `vec (*, /, *=, /=) vec` -- Multiplies cooresponding components
* `vec (*, /, *=, /=) R  ` -- Multiplies components by a scalar
* `vec (<, >, <=, >=) vec` -- Compares magnitudes
* `vec (==, !=) vec      ` -- Compares each cooresponding component
* `vec[]                 ` -- Reference individual elements
* `ostream << vec        ` -- Stream insertion

Functions:

* `R magsquared(vec)     ` -- Returns the square of a vector's magnitude (faster to compute than `mag` for comparisons)
* `R mag(vec)            ` -- Returns the magnitude of a vector
* `vec unit(vec)         ` -- Returns the normalized version of a vector (without changing it)
* `normalize(vec)        ` -- Normalizes a vector (changing it)
* `R dot(vec, vec)       ` -- Returns the dot product of two vectors
* `float angle(vec, vec) ` -- Returns the angle in radians between two vectors
* `vec3 cross(vec3, vec3)` -- Returns the cross product of two vectors (3D only)

Geometry
========
Basic geometric shape types and algorithms for intersection tests/results and other useful queries.
Intersection test algorithms return true or false.
Intersection result algorithms return the relevant shape of the intersection.
Depends on Linear Algebra

	#include "geometry.h"
	using namespace hmath;
	typedef vec<2,float> Vec;
	typedef line<2,float> Line;
	
	int main ()
	{
		// Define two line segments
		Line a(Vec(3, -1), Vec(0, 6));
		Line b(Vec::origin(), Vec(4, 5));
		
		// Intersection test
		if (touching(a, b))
		{
			// Intersection result
			cout << intersection(a, b) << endl;
		}
	}

Geometry: Types
---------------

* `line<int N, class R>` -- ND, two intersecting points
* `circle<class R>`      -- 2D, center point and radius
* `rect_aa<class R>`     -- 2D, axis aligned, center point and x/y radii
* 2D polygons can be represented by a container/array of edge points in order of connectivity - functions that use them are templated to take objects fulfilling the [Iterator concept](http://en.cppreference.com/w/cpp/concept/Iterator) similar to [std::sort()](http://www.cplusplus.com/reference/algorithm/sort/).

Geometry: Operators and Functions
---------------------------------
`R` -- Scalar template parameter type.  All operators and functions work for any template size and type unless otherwise stated.

* `bool is_left(vec, line)` -- 2D, Returns true if a point is on the left side of a line
* `vec normal(line)` -- 2D, Return the normal vector of a line (magnitude proportional to the length of the segment)
* `bool touching(VecIterator, VecIterator, vec)` -- 2D, Returns true if a point is inside a polygon

Statistics
==========
Useful statistics algorithms.

	#include <iostream>
	#include <vector>
	#include <hmath/statistics.h>
	using namespace hmath;
	using namespace std;


	int main (int argc, char const* argv[])
	{
		float a[4] = {3.4, 5.3, 4.3, 3.8};
		vector<float> v(a+0, a+4);
		
		cout << "mean with pointers: "  << mean(a+0, a+4)                         << endl;
		cout << "mean with iterators: " << mean(v.begin(), v.end())               << endl;
		cout << "variance: "            << variance(v.begin(), v.end())           << endl;
		cout << "standard_deviation: "  << standard_deviation(v.begin(), v.end()) << endl;
	
		return 0;
	}

Output:

	mean with pointers: 4.2
	mean with iterators: 4.2
	variance: 0.505
	standard_deviation: 0.710634

Statistics: Functions
---------------------
`R` -- Numeric type.

* `R mean(InputIterator, InputIterator)` -- Calculate the mean of a range of values
* `R variance(InputIterator, InputIterator)` -- Calculate the variance of a range of values
* `R standard_deviation(InputIterator, InputIterator)` -- Calculate the standard deviation of a range of values
