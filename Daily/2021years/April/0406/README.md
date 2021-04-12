## 1. 목적

프로젝트를 진행하다보니 모양이 같은 카드를 여러 곳에서 사용하는 것을 확인하였다.

![Untitled (7)](https://user-images.githubusercontent.com/58289110/114331517-28a53680-9b7f-11eb-967f-8329577f600a.png)

![Untitled (8)](https://user-images.githubusercontent.com/58289110/114331523-2c38bd80-9b7f-11eb-85d3-6f021bb358e0.png)


해당 카드들을 퍼블리싱에서는 공통으로 사용하지만, 

프론트 영역에서는 서로 다른 개발자들이 개발을 하다보니 각각의 컴포넌트 속 각각의 카드가 존재하였고, 같은 퍼블리싱 코드가 반복되는 것은 비효율적이라는 생각이 들어 카드 공통화 작업을 시작 하였다.

## 어떻게??

일단은 카드의 퍼블리싱을 검토하는게 우선이였다.

![Untitled (9)](https://user-images.githubusercontent.com/58289110/114331531-2fcc4480-9b7f-11eb-9417-878f9f523bea.png)

위 코드를 보면,

카드 본체 부분은 list-a-wrap 클래스로 감싸져 공통으로 사용하고 있어서 공통으로 사용하기 적합하였으나,

![Untitled (14)](https://user-images.githubusercontent.com/58289110/114331535-30fd7180-9b7f-11eb-8208-8f16a8506275.png)

상단에 전체를 감싸는 sec-inner 라는 클래스가 페이지별 padding을 주고 있어서 내부에 wrap에 스타일을 공통화해도 각각 페이지별 padding이 달라지는 오류가 발생하였다.

다행히(?) 우리 프로젝트는 스타일을 module.scss를 사용하여 import하는 구조였어서 상단의 sec-inner 클래스의 각각의 스타일을 다르게 import해주고 하단의 list-wrap부분을 공통화 해주면 될 것 같다는 생각을 하였다.

## 해보자!

결론적으로 되었다!

코드를 보자!

 index.tsx (카드가 존재하는 페이지)

```jsx
import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_mainpurc.module.scss';
import cardStyles from 'src/styles/scss/modules/_list-type-a.module.scss';

const cx = classNames.bind(styles);
const cx2 = classNames.bind(cardStyles);

function MainCustReco(): React.ReactElement {

const { custList } = useSelector((state: RootState) => {
    return {
      custList: state.main.custGoods,
    };
  });

return(
				<div className={cx('sec-inner', 'mb50')}>
          <h2 className={cx('title-link')}>
            {custList[0].nickname}님을 위한 맞춤 추천
          </h2>
          <div className={cx2('list-a-wrap')}>
            <ul className={cx2('list-a')} style={{ paddingLeft: '24px' }}>
              {custList.map((goods, i) => {
                return <GoodsCardMedium key={i} goodsInfo={goods} />;
              })}
            </ul>
          </div>
        </div>
)}
```

위와 같이 스타일을 cx, cx2로 구분하여 import하여 스타일을 분리해주고,

간혹 퍼블리싱이 적용안되는 경우 퍼블리셔분께 추가요청을 드려야하나 외주업체인 관계로 인라인 스타일로 적용해주었다. (style={{ paddingLeft: '24px' }})

GoodsCardMedium.tsx

```jsx
import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_list-type-a.module.scss';

const cx = classNames.bind(styles);

// Origin : list-type-a01.html
function GoodsCardMedium(props: Props): React.ReactElement {
return (
    <>
      <li>
        <div className={cx('thumb')}>
          <a onClick={handleClickGoods}>
            {best && <span className={cx('num')}>{best}</span>}
            <img src={imgUrl} alt="상품 썸네일 이미지" />
          </a>
          <LikeBtn
            type={'card'}
            goodsNo={goodsNo}
            saleNo={saleNo}
            favorYn={favorYn}
          />
        </div>
        <div className={cx('cert')}>
          <i className={cx('icon', 'cert-badge1', icon)} />
          <span className={cx('name')}>{certNm}</span>
        </div>
        <div className={cx('product-name')}>
          <a className={cx('ellipsis')}>{goodsNm}</a>
        </div>
        <div className={cx('product-price')}>
          <a>
            <span className={cx('num')}>{commafy(saleAmt)}</span>
            <span className={cx('won')}>원</span>
          </a>
        </div>
        <div className={cx('info-badge')}>
          <span className={cx('tag', kbnMsg === 'refer' ? kbnMsg : 'unopened')}>
            <i className={cx('icon', 'icon-' + kbnMsg)} />
            <span className={cx('blind')}>{goodsKbn}</span>
          </span>
        </div>
      </li>
    </>
  );
}
```

카드를  GoodsCardMedium.tsx로 컴포넌트를 분리해 주면 여러 곳에서 호출해서 사용가능한 카드가 만들어진다.

![Untitled (11)](https://user-images.githubusercontent.com/58289110/114331546-365abc00-9b7f-11eb-9f80-37ae485cbee9.png)

각 폴더별로 카드가 존재하였는데, 아래와 같이 공통 카드로 common 폴더에 빼두고 사용하니 더 작업이 편해졌다.

![Untitled (12)](https://user-images.githubusercontent.com/58289110/114331547-378be900-9b7f-11eb-99c0-a5e0321c4aa9.png)

찜하기 버튼, 공통타입들도 동시에 공통화를 하여 전체적인 코드가 한결 깔끔해져서 앞으로도 생각하면서 코딩을 해야겠다는걸 깨달았다.

![Untitled (13)](https://user-images.githubusercontent.com/58289110/114331551-3b1f7000-9b7f-11eb-8ffa-53a7d2db0d8f.png)

