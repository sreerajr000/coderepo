---
layout: post
author: Sreeraj
title: Generate Random Point in a Circle
---

Given the radius and x-y positions of the center of a circle, write a function randPoint which generates a uniform random point in the circle.

```cpp
class Solution {
public:
    double x, y, r;
    uniform_real_distribution<double> dist;
    default_random_engine generator;

    Solution(double radius, double x_center, double y_center) {
        x = x_center;
        y = y_center;
        r = radius;
        dist = uniform_real_distribution<double>(0, 1);
    }
    
    vector<double> randPoint() {
        double theta = 2 * M_PI * (dist(generator) - 0.5);
        double r1 = sqrt(dist(generator));
        double x1 = r1 * cos(theta) * r;
        double y1 = r1 * sin(theta) * r;
        return vector<double>({x+x1, y+y1});
    }
};
```

```cpp
class Solution {
public:
    double x, y, r;
    uniform_real_distribution<double> dist;
    default_random_engine generator;

    Solution(double radius, double x_center, double y_center) {
        x = x_center;
        y = y_center;
        r = radius;
        dist = uniform_real_distribution<double>(-r, r);
    }
    
    vector<double> randPoint() {
        double p,q;
        while(true) {
            p = dist(generator);
            q = dist(generator);
            if(pow(p,2.0)+pow(q,2.0) <= pow(r,2.0))
                break;
        }
        return vector<double>({x+p,y+q});
    }
};
```