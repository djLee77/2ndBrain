Box Shadow
----------------------

기본 구문

```
box-shadow: [horizontal offset] [vertical offset] [blur radius] [optional spread radius] [color];
```


1. **horizontal offset (수평 오프셋)**: 그림자가 요소의 어느 방향으로 수평으로 얼마나 떨어져 있는지를 지정합니다. 양수 값은 그림자를 요소의 오른쪽으로, 음수 값은 왼쪽으로 이동시킵니다.
    
2. **vertical offset (수직 오프셋)**: 그림자가 요소의 어느 방향으로 수직으로 얼마나 떨어져 있는지를 지정합니다. 양수 값은 그림자를 요소의 아래로, 음수 값은 위로 이동시킵니다.
    
3. **blur radius (흐림 반경)**: 그림자의 흐림 정도를 지정합니다. 값이 클수록 그림자가 더 흐릿하게 보입니다. 0 값을 가지면 그림자는 흐릿하지 않습니다.
    
4. **spread radius (확산 반경) (옵션)**: 그림자의 크기를 확장하거나 축소하는데 사용됩니다. 양수 값은 그림자를 확장시키고, 음수 값은 축소시킵니다.
    
5. **color**: 그림자의 색상을 지정합니다.

예시

```
.box {
  box-shadow: 3px 3px 5px 0px gray;
}
```
