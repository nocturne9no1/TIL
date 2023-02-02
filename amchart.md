# amchart

## XYChart

### Date Axis

#### 날짜 변경 시 영문 안나오게 하기

* default 설정대로 진행 시 다음과 같이 영문으로 날짜 단위 표시됨

![image-20221129150626543](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20221129150626543.png)

* 다음의 속성으로 안나오게 가능

```tsx
let xAxis = chart.xAxes.push(
  am5xy.DateAxis.new(root, {
    baseInterval: { timeUnit: "day", count: 1 },
    markUnitChange: false,  // 날짜 변경 방지 속성 값
    renderer: am5xy.AxisRendererX.new(root, {})
  })
);
```

결과값

![image-20221129150711032](/Users/nocturne9no1/Library/Application Support/typora-user-images/image-20221129150711032.png)