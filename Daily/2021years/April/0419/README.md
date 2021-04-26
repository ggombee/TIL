```jsx
//입력 여부 확인
useEffect(() => {
  accInfo.accNum && accInfo.bnkCd ? setConfirm(true) : setConfirm(false);
 }, [accInfo]);

//입력 여부 확인
useEffect(() => {
   setConfirm(
     Object.values(accInfo).every(v => v.length > 0) &&
       Boolean(accInfo.accNum.trim()),
   );
 }, [accInfo]);
```

shema validation

class-validator

ajv나

const isReady = useMemo(() => Object.values)

for-of로
