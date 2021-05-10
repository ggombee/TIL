```jsx
//수정완료 버튼 활성화
  useEffect(() => {
    //상품이미지 리스트 존재
    if (
      productImgUrlList.length + productLoadAwsList.length > 0 &&
      !!price &&
      !!gdDesc &&
      !!name
    ) {
      //이름필수
      if (name.length > 0 && name.length < 31) {
        //설명필수
        if (gdDesc.length > 0 && gdDesc.length < 2001) {
          //가격필수
          if (price.length > 0 && price.length < 11) {
            setIsReady(true);
          } else {
            setIsReady(false);
          }
        } else {
          setIsReady(false);
        }
      } else {
        setIsReady(false);
      }
    } else {
      setIsReady(false);
    }
  }, [price, gdDesc, productImgUrlList, name, productLoadAwsList]);

  const onChangeText = e => {
    if (e.target.id === 'text') {
      e.target.value.length < 32
        ? setName(e.currentTarget.value)
        : setName(name);
    } else if (e.target.id === 'desc') {
      e.target.value.length < 2002
        ? setGdDesc(e.currentTarget.value)
        : setGdDesc(gdDesc);
    } else if (e.target.id === 'hash') {
      Object.values(String(e.currentTarget.value).split('#')).every(
        v => v.length < 11,
      )
        ? setTag(e.currentTarget.value)
        : alert('해시태그는 10자 이내로 작성해주세요.');
    } else if (e.target.id === 'price') {
      e.target.value.length < 12
        ? setPrice(e.currentTarget.value)
        : setPrice(price);
    }
  };
```
