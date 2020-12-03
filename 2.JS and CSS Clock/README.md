## 1. transform-origin

> CSS transform 속성과 함께 사용되는 속성
>
> default : 50% 50% (요소의 중심점)

- 회전 중심(== 원점 == 기준점)을 지정

- rotate(), skew() 등의 회전, 변형 속성을 사용하기 전에 기준점을 지정해 둠

- 속성 값은 백분율(%)과 키워드 중 하나로 지정할 수 있음



| 백분율(%) | **## 1. transform-origin**대응 가능한 키워드                 |
| --------- | ------------------------------------------------------------ |
| 0%        | \- CSS transform 속성과 함께 사용되는 속성left               |
| 0%        | \- 회전 중심(== 원점 == 기준점)을 지정top                    |
| 50%       | \- rotate(), skew() 등의 회전, 변형 속성을 사용하기 전에 기준점을 지정해 둠center |
| 100%      | \- 초기 값 : 50% 50% (요소의 중심점)right                    |
| 100%      | \- 속성 값은 백분율(%)과 키워드 중 하나로 지정할 수 있음bottom |



| 백분율(%) | 대응 가능한 키워드                           |
| --------- | -------------------------------------------- |
| 0% 0%     | [top left] / [left top]                      |
| 0% 50%    | [left] / [left center] / [center left]       |
| 50% 0%    | [top] / [top center] / [center top]          |
| 0% 100%   | [bottom left] / [left bottom]                |
| 100% 0%   | [right top] / [ top right]                   |
| 50% 100%  | [bottom] / [bottom center] / [center bottom] |
| 100% 50%  | [right] / [right center] / [center right]    |
| 100% 100% | [bottom right] / [right bottom]              |



[출처](https://www.tabmode.com/homepage/transform-origin.html#gsc.tab=0)