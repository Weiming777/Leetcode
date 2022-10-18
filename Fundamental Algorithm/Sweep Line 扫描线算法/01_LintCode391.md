# Number of Airplanes in the sky

![image-20221018105714104](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018105714104.png)

![image-20221018105741991](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018105741991.png)



![image-20221018105808124](/Users/weimingqi/Library/Application Support/typora-user-images/image-20221018105808124.png)



```java
public int countOfAirplanes(list<Interval> airplanes) {
  List<point> list = new ArralyList<>(airplanes.size() * 2);
  for (Interval i: airplanes) {
    list.add(new point(i.start, 1));
    list.add(new point(i.end, -1));
  }
  
  Collections.sort(list, (point p1, point p2)->{if p1.T == p2.T} return p1.S - p2.S; return p1.T - p2.T;});
  
  int cut = 0;
  int ans = 0;
  for (point p: list) {
    if (p.S == 1) cnt++;
    else cnt--;
    ans = Math.max(ans, cnt);
  }
  
  return ans;
}
```

