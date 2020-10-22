# useMemo - useCallback

나는 지금까지 useMemo 내에서 참조하고 있는 값이라면 무조건 dependency가 되는 줄 알았음.

![deps warning](./1.png)

역시 openBulkAddModal을 deps array에서 제거시키나까 warning이 뜨는구만 허허.

![clear](./2.png)

그런데 openBulkAddModal에서 useCallback을 제거하니 deps array에서 warning이 없어졌다??

[돌아가기](/README.md)
