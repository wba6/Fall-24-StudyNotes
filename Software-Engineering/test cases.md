- **Test case for precondition: both vector lengths are the same**
	- **Parameter values** 
		- V1 = {4, 5, 6} 
		- V2 = {4, 5, 6, 5} 
	- **Expected answer** 
		- 0.0 
	- **Lines of code covered** 
	```
	    if (v1.size() != v2.size()) {
	        return 0.0;
	    }
	```
	- **The percentage coverage of `dotProduct` by this test case**
		-  Of 24 lines of code within the function this test case covers 3 giving it 12.5 percent coverage

- **Test case for precondition: first vector is not empty**
	- **Parameter values** 
		- V1 = {}
		- V2 = {1, 2, 3} 
	- **Expected answer** 
		- 0.0 
	- **Lines of code covered** 
	```
	    if (v1.empty()) {
	        return 0.0;
	    }
	```
	- **The percentage coverage of `dotProduct` by this test case**
		-  Of 24 lines of code within the function this test case covers 3 giving it 12.5 percent coverage

- **Test case for precondition: first vector is not all zeroes** 
	- **Parameter values** 
		- V1 = {0, 0, 0} 
		- V2 = {4, 5, 6} 
	- **Expected answer** 
		- 0.0 
	- **Lines of code covered** 
	```
		const auto nonZeroPositionV1 = std::find_if(v1.begin(), v1.end(), [](double x){ return x != 0; });
	    if (nonZeroPositionV1 == v1.end()) {
	        return 0.0;
	    }
	```
	- **The percentage coverage of `dotProduct` by this test case**
		-  Of 24 lines of code within the function this test case covers 4 giving it approximately 16 percent coverage

- **Test case for precondition: first vector is not all zeroes** 
	- **Parameter values** 
		- V1 = {4, 5, 6} 
		- V2 = {0, 0, 0} 
	- **Expected answer** 
		- 0.0 
	- **Lines of code covered** 
	```
		const auto nonZeroPositionV2 = std::find_if(v2.begin(), v2.end(), [](double x){ return x != 0; });
	    if (nonZeroPositionV2 == v2.end()) {
	        return 0.0;
	    }
	```
	- **The percentage coverage of `dotProduct` by this test case**
		-  Of 24 lines of code within the function this test case covers 4 giving it approximately 16 percent coverage

- **Test case for the dot product of the two vectors** 
	- **Parameter values** 
		- V1 = {1, 2, 3} 
		- V2 = {4, 5, 6} 
	- **Expected answer** 
		- 32.0 
	- **Lines of code covered** 
	```
		double result = 0.0;
	    std::vector<double>::size_type i = 0;
	    while (i < v1.size()) {
	        result += v1[i] * v2[i];
	        ++i;
	    }
	    return result;
	```
	- **The percentage coverage of `dotProduct` by this test case**
		-  Of 24 lines of code within the function this test case covers 7 giving it approximately 29 percent coverage

**Note:** Our test cases only cover 21 of the 24 lines of code this is because the following code is unreachable within the function.
```
    // precondition: second vector is not empty
    if (v2.empty()) {
        return 0.0;
    }
```