## 1. 목표

### 버튼 클릭시 이미지를 해당 앱에 업로드 후 미리	보기로 보여준뒤, 저장하는 시점에 aws에 업로드 한다.

처음부터 aws에 업로드 하지않는 이유는 사용자가 이미지를 넣었다 뺏다 하는 UI 이기 때문에, 많은 서용자가 동시 다발적으로 업로드시 부하가 발생할 수 있기 때문이다.

## 순서

### input button에 파일 열기 기능 추가

퍼블리싱이  input box가 아닌 button으로 나와 임의로 input box에 함수를 추가하여 로직을 구성하였다.

```jsx
{/*파일 불러오기*/}
								<input
                  id="inputPhotoProduct"
                  type="file"
                  accept="image/*"
                  // onChange={e => choiceProductImg(e)}
                  onChange={onCustomThumbSelect}
                  style={{ display: 'none' }}
                />
								<button
                  className={cx('btn', 'btn-add-photo')}
                  onClick={handleClickImgPlus}
                >
                  <i className={cx('icon', 'icon-camera-gray')} />
                  <span className={cx('count')}>
                    <span className={cx('current')}>
                      {productImgUrlList.length}
                    </span>
                    <span>/</span>
                    <span className={cx('total')}>10</span>
                  </span>
                </button>
```

 

### 이미지 미리보기 기능 구현

함수 consthandleClickImgPlus , onCustomThumbSelect 

```jsx
//사진선택 input커스텀
consthandleClickImgPlus = () => {
//이어서 하기인 경우
if(productImgAwsList.length > 0) {
constanwer = window.confirm(
      '기존 이미지는 삭제되고 새로 등록됩니다. 삭제 후 새로 등록하시겠습니까?',
    );
if(anwer) {
//aws이미지 삭제데이터 별도저장

const_productImgAwsList = productImgAwsList;
      setDeleteImgAwsList(deleteImgAwsList.concat(_productImgAwsList));
      setProductImgAwsList([]);
      setProductImgUrlList([]);
      setProductImgFileList([]);
    }
  }else{
//최대 등록 개수 체크
constisProductCnt = productImgUrlList.length + 1 > 10;

if(isProductCnt) {
alert(
        '상품사진 등록 최대 개수를 초과하였습니다. 삭제 후 등록 해주세요.',
      );
return;
    }
    photoInputClick();
  }
};

//이미지 미리보기
  const onCustomThumbSelect = (e: any) => {
    const file = e.target.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.readAsDataURL(file);
    reader.onloadend = () => {
      const readerImge = [reader.result];
      const readFile = [file];
      setProductImgUrlList(readerImge.concat(productImgUrlList));
      setProductImgFileList(readFile.concat(productImgFileList));
    };
  };

```

### 이미지 미리보기 삭제 기능 구현

```jsx
//이미지 미리보기 선택 삭제
  const onCustomThumbDelete = (index: number) => {
    setImgType('start');
    productImgUrlList.splice(index, 1);
    productImgFileList.splice(index, 1);
    setTimeout(() => {
      setImgType(''); //삭제완료 시점 render 타이밍
    }, 150);
  };
```

### 확인 버튼 클릭 시 aws 이미지 저장

시점문제가 발생 할 수 있어 버튼 클릭시  aws이미지를 등록하고 동시에 state에 이미지 리스트를 받아와서 useEffect로 이미지 리스트가 있을때 확인 api를 쏘는 구조로 로직을 짰다.

```jsx
//다음 aws url저장 후 api 호출
  useEffect(() => {
    if (!isNextClick) return;

    //aws 등록 후 url 타이밍 맞추는 조건

    const isProduct =
      //수정하기 경우
      queryParams.goodsNo && productImgAwsList.length > 0
        ? true
        : //상품 파일/url 갯수가 같으면 ture
        productImgAwsList.length > 0 &&
          productImgAwsList.length === productImgFileList.length
        ? true
        : false;

    if ((queryParams.goodsNo && isProduct) || isProduct) {
       api
      .post('/review', {param})
      .then(() => {
      history.push({
        pathname: '/goodsdetail',
        search: `?goodsNo=${goodsNo}&saleNo=${saleNo}`,
      });
      dispatch(isToastPop(true));
      dispatch(getPopText('거래 후기가 등록되었습니다.'));

      //     })
      //     .finally(() => setIsNextClick(false));
    }
  }, [
    history,
    productImgAwsList,
    productImgFileList.length,
    queryParams.goodsNo,
  ]);
```

![image](https://user-images.githubusercontent.com/58289110/114329641-d82bda00-9b7a-11eb-8622-274278fb471c.png)
