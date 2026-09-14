https://en.cppreference.com/w/cpp/language/decltype.html
```cpp
#include <cassert>
#include <iostream>
#include <type_traits>
 
struct A { double x; };
const A* a;
 
decltype(a->x) y;       // type of y is double (declared type)
decltype((a->x)) z = y; // type of z is const double& (lvalue expression)
 
template<typename T, typename U>
auto add(T t, U u) -> decltype(t + u) // return type depends on template parameters
                                      // return type can be deduced since C++14
{
    return t + u;
}
 
const int& getRef(const int* p) { return *p; }
static_assert([std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(getRef), const int&(const int*)>);
auto getRefFwdBad(const int* p) { return getRef(p); }
static_assert([std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(getRefFwdBad), int(const int*)>,
    "Just returning auto isn't perfect forwarding.");
decltype(auto) getRefFwdGood(const int* p) { return getRef(p); }
static_assert([std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(getRefFwdGood), const int&(const int*)>,
    "Returning decltype(auto) perfectly forwards the return type.");
 
// Alternatively:
auto getRefFwdGood1(const int* p) -> decltype(getRef(p)) { return getRef(p); }
static_assert([std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(getRefFwdGood1), const int&(const int*)>,
    "Returning decltype(return expression) also perfectly forwards the return type.");
 
int main()
{
    int i = 33;
    decltype(i) j = i * 2;
    static_assert([std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(i), decltype(j)>);
    [assert](https://en.cppreference.com/w/cpp/error/assert.html)(i == 33 && 66 == j);
 
    auto f = [i](int av, int bv) -> int { return av * bv + i; };
    auto h = [i](int av, int bv) -> int { return av * bv + i; };
    static_assert(![std::is_same_v](https://en.cppreference.com/w/cpp/types/is_same.html)<decltype(f), decltype(h)>,
        "The type of a lambda function is unique and unnamed");
 
    decltype(f) g = f;
    [std::cout](https://en.cppreference.com/w/cpp/io/cout.html) << f(3, 3) << ' ' << g(3, 3) << '\n';
}
```
