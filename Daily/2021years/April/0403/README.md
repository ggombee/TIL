## 로그인을 했을때, 안했을때,,,,,

작업을 하다보니 까다로운 조건문을 작성해야 할일이 생겼다...

상품상세페이지를 판매자와 구매자(로그인상태/비로그인상태) 모두 볼수 있는데 구분을 해서  하단 푸터 스타일이 바뀌어야 했다.

api는 상품의 상태코드(00: 판매대기, 01: 판매등록, 02: 거래중, 03: 판매완료)와 접속한 사람의 상태코드(S: 판매자, B: 구매자)가 내려오는 상황이다.

처음에는 멘붕이었지만,,, 코드의 변천사...? 를 기록해야겠다.

초기 코드는 삼항조건문의 중첩중첩 헬파티다...

## 1. 초기 상태(헬파티)

### DetailFooter.tsx

```java
import React, { useState } from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';
import { RootState } from '../../stores/rootReducer';
import { useSelector, useDispatch } from 'react-redux';

const cx = classNames.bind(styles);

interface Props {
  handleClickLike: () => void;
  handleClickQuestion: () => void;
  isLike: boolean;
}

function DetailFooter(props: Props): React.ReactElement {
  const { isLike, handleClickLike, handleClickQuestion } = props;
  const { goodsInfo } = useSelector((state: RootState) => {
    return {
      goodsInfo: state.goodsdetail.goodsInfo,
    };
  });

  const { statusCd, myUserType, ordSttsCd } = goodsInfo;
  // (00: 판매대기, 01: 판매등록, 02: 거래중, 03: 판매완료)
  return (
    <>
      {/*adminId !== sellerId, buyerId  -- 접속한 사람이(로그인,비로그인) 구매자 판매자 모두 아닐경우*/}
      {/*adminId === buyerId  -- 접속한 사람이(로그인) 구매자 인 경우*/}
      {!myUserType ||
        (myUserType === 'B' && (
          <div className={cx('area-footer')}>
            <div className={cx('icon-box')}>
              <button
                type="button"
                className={cx(
                  'btn',
                  'btn-empty',
                  'btn-like',
                  isLike ? 'on' : '',
                )}
                onClick={handleClickLike}
              >
                <i className={cx('icon', 'icon-like-32')} />
                <span className={cx('blind')}>찜하기</span>
              </button>
            </div>

            {statusCd === '02' || statusCd === '00' ? (
              <div className={cx('btn-group')}>
                <button
                  type="button"
                  className={cx('btn', 'btn-main')}
                  onClick={handleClickQuestion}
                >
                  문의하기
                </button>
              </div>
            ) : statusCd === '01' ? (
              <div className={cx('btn-group')}>
                <button
                  type="button"
                  className={cx('btn', 'btn-default')}
                  onClick={handleClickQuestion}
                >
                  문의하기
                </button>
                <button type="button" className={cx('btn', 'btn-main')}>
                  결제하기
                </button>
              </div>
            ) :
              ordSttsCd ==='08'?(
              <div className={cx('btn-group')}>
                <button type="button" className={cx('btn', 'btn-main')}>
                  거래후기 쓰러가기
                </button>
              </div>):( <div className={cx('btn-group')}>
                <button
                  type="button"
                  className={cx('btn', 'btn-default')}
                  onClick={handleClickQuestion}
                >
                  문의하기
                </button>
                <button type="button" className={cx('btn', 'btn-main')}>
                  구매확정
                </button>
              </div>
            )}
          </div>
        ))}

      {/*adminId === buyerId  -- 접속한 사람이(로그인) 판매자 인 경우*/}
      {myUserType === 'S' && (
        <div className={cx('area-footer', 'seller-btn')}>
          <div className={cx('btn-group', 'two-btn')}>
            <button
              type="button"
              className={cx('btn', 'btn-default')}
              onClick={handleClickQuestion}
            >
              <i className={cx('icon', 'icon-request-delivery')} />
              <span>택배 신청</span>
            </button>
            <button type="button" className={cx('btn', 'btn-default')}>
              <i className={cx('icon', 'icon-deal-cancel')} />
              <span>거래 취소</span>
            </button>
          </div>
        </div>
      )}
    </>
  );
}

export default DetailFooter;
```

코딩을 하나보니 중첩문이 여러개 반복되어 헷갈려서 가독성이 좋지 않을 뿐더러,, 스타일이 여러개라 같은 것이 반복되는 부분과 처리함에 있어서 불편함이 발생하였다.

그래서 다시 코드를 짜기로 했다..

하단의 버튼 영역만 분리해서 SellerBtn.tsx와 BuyerBtn.tsx로 분리하였다.

 

## 2. 컴포넌트 분리 (푸터클린)

### DetailFooter.tsx

```java
import React, { useState } from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';
import { RootState } from '../../stores/rootReducer';
import { useSelector, useDispatch } from 'react-redux';
import SellerBtn from 'src/component/Goods/SellerBtn';
import BuyerBtn from '../../component/Goods/BuyerBtn';
const cx = classNames.bind(styles);

interface Props {
  handleClickLike: () => void;
  handleClickQuestion: () => void;
  isLike: boolean;
}

function DetailFooter(props: Props): React.ReactElement {
  const { isLike, handleClickLike, handleClickQuestion } = props;
  const { goodsInfo } = useSelector((state: RootState) => {
    return {
      goodsInfo: state.goodsdetail.goodsInfo,
    };
  });

  const { statusCd, myUserType, ordSttsCd } = goodsInfo;
  return (
    <>
      {!myUserType || myUserType === 'B' ? (
        <>
          {/* 해당 상품의 판매자 인 경우*/}
          <div className={cx('area-footer')}>
            <div className={cx('icon-box')}>
              <button
                type="button"
                className={cx(
                  'btn',
                  'btn-empty',
                  'btn-like',
                  isLike ? 'on' : '',
                )}
                onClick={handleClickLike}
              >
                <i className={cx('icon', 'icon-like-32')} />
                <span className={cx('blind')}>찜하기</span>
              </button>
            </div>

            <div className="btn-group">
              <BuyerBtn type={statusCd} />
            </div>
          </div>
        </>
      ) : (
        <>
          {/* 해당 상품의 판매자 인 경우*/}
          <div className={cx('area-footer', 'seller-btn')}>
            <div className={cx('btn-group', 'two-btn')}>
              <SellerBtn type={statusCd} />
            </div>
          </div>
        </>
      )}
    </>
  );
}

export default DetailFooter;
```

해당 파일에서 각각 판매자와 구매자의 버튼 스타일이 달라서 구분을 하고 각 컴포넌트의 진입 후 분기를 위한 type을 props로 내려주었다.

### BuyerBtn.tsx

```java
import React from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';

const cx = classNames.bind(styles);

interface Props {
  type: string;
}

function BuyerBtn(props: Props): React.ReactElement {
  const { type } = props;

  return (
    <>
      {/*일반상품일경우  01: 판매등록*/}
      {type === '01' ? (
        <>
          <button type="button" className={cx('btn', 'btn-default')}>
            문의하기
          </button>
          <button type="button" className={cx('btn', 'btn-main')}>
            결제하기
          </button>
        </>
      ) : (
        <>
          {/*00: 판매대기, 02: 거래중
           거래중 */}
          {type === '00' || type === '02' ? (
            <>
              <button type="button" className={cx('btn', 'btn-main')}>
                문의하기
              </button>
            </>
          ) : (
            <>
              {/*03: 판매완료*/}

              <button type="button" className={cx('btn', 'btn-default')}>
                문의하기
              </button>
              <button type="button" className={cx('btn', 'btn-main')}>
                결제하기
              </button>
            </>
          )}
        </>
      )}
    </>
  );
}

export default BuyerBtn;
```

### SellerBtn.tsx

```java
import React from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';

const cx = classNames.bind(styles);

interface Props {
  type: string;
}

function SellerBtn(props: Props): React.ReactElement {
  const { type } = props;

  return (
    <>
      {/*일반상품일경우  01: 판매등록*/}
      {type === '01' ? (
        <>
          <button
            type="button"
            className={cx('btn btn-default')} >
            <i className={cx('icon', 'icon-state-change')}/>
            <span>상태 변경</span>
          </button>
          <button type="button" className={cx('btn', 'btn-default')}>
            <i className={cx('icon', 'icon-content-change')}/>
            <span>내용 수정</span>
          </button>
          <button
            type="button"
            className={cx('btn', 'btn-default')}
          >
            <i className={cx('icon', 'icon-product-delete')}/>
            <span>상품 삭제</span>
          </button>
        </>
      ) : (
        <>
          {/*00: 판매대기*/}
          {type === '00' && (
            <>
              <button
                type="button"
                className={cx('btn', 'btn-default')}>
                <i className={cx('icon', 'icon-state-change')}/>
                <span>상태 변경</span>
              </button>
              <button type="button" className={cx('btn', 'btn-default')}>
                <i className={cx('icon','icon-content-change')}/>
                <span>내용 수정</span>
              </button>
              <button
                type="button"
                className={cx('btn', 'btn-default')}
              >
                <i className={cx('icon', 'icon-product-delete')}/>
                <span>상품 삭제</span>
              </button>
            </>
          )}
          {/*02: 거래중인 상품 */}
          {type === '02' && (
            <>
              <button
                type="button"
                className={cx('btn', 'btn-default')}
                // onClick={handleClickQuestion}
              >
                <i className={cx('icon', 'icon-request-delivery')} />
                <span>택배 신청</span>
              </button>
              <button type="button" className={cx('btn', 'btn-default')}>
                <i className={cx('icon', 'icon-deal-cancel')} />
                <span>거래 취소</span>
              </button>
            </>
          )}
          {/* 03: 판매완료*/}
          {type === '03' && (
            <>
              <button type="button" className={cx('btn', 'btn-default' )}>
                <i className={cx('icon', 'icon-product-delete')}/>
                <span>상품 삭제</span>
              </button>
            </>
          )}
        </>
      )}
    </>
  );
}

export default SellerBtn;
```

DetailFooter.tsx의 코드가 비교적 가독성이 괜찮아졌지만, 여전히 각 Btn.tsx에서의 같은 jsx스타일들이 반복되는 문제는 해결 되지않았다.

그러던 중 switch case문을 이용한 조건부 렌더링이 가능하다는 사실을 알게 되어서,

switch case문을 이용해 return 값을 달리해주도록 변경하였다.

## 3. Swtich case!!

### SellerBtn.tsx

```java
import React from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';

const cx = classNames.bind(styles);

interface Props {
  type: string;
}

function SellerBtn(props: Props): React.ReactElement {
  const { type } = props;

  switch (type) {
    case '00':
    case '01':
      return (
        <>
          <button type="button" className={cx('btn btn-default')}>
            <i className={cx('icon', 'icon-state-change')} />
            <span>상태 변경</span>
          </button>
          <button type="button" className={cx('btn', 'btn-default')}>
            <i className={cx('icon', 'icon-content-change')} />
            <span>내용 수정</span>
          </button>
          <button type="button" className={cx('btn', 'btn-default')}>
            <i className={cx('icon', 'icon-product-delete')} />
            <span>상품 삭제</span>
          </button>
        </>
      );
    case '02':
      return (
        <>
          <button
            type="button"
            className={cx('btn', 'btn-default')}
            // onClick={handleClickQuestion}
          >
            <i className={cx('icon', 'icon-request-delivery')} />
            <span>택배 신청</span>
          </button>
          <button type="button" className={cx('btn', 'btn-default')}>
            <i className={cx('icon', 'icon-deal-cancel')} />
            <span>거래 취소</span>
          </button>
        </>
      );
    case '03':
      return (
        <>
          <button type="button" className={cx('btn', 'btn-default')}>
            <i className={cx('icon', 'icon-product-delete')} />
            <span>상품 삭제</span>
          </button>
        </>
      );
    default:
      return <></>;
  }
}

export default SellerBtn;
```

### BuyerBtn.tsx

```java
import React from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';

const cx = classNames.bind(styles);

interface Props {
  type: string;
}

function BuyerBtn(props: Props): React.ReactElement | null {
  const { type } = props;

  switch (type) {
    case '01':
    case '03':
      return (
        <>
          <button type="button" className={cx('btn', 'btn-default')}>
            문의하기
          </button>
          <button type="button" className={cx('btn', 'btn-main')}>
            결제하기
          </button>
        </>
      );
    case '02':
    case '00':
      return (
        <>
          <button type="button" className={cx('btn', 'btn-main')}>
            문의하기
          </button>
        </>
      );
    default:
      return null;
  }
}

export default BuyerBtn;
```

하....코드가 편안해 졌다....

위에서는 다른조건이여도 스타일이 같으면 중복으로 작성되는 경우가 발생하였는데, 

switch case문으로 같은 스타일이면 한번만 작성될 수 있도록!!! 바뀌어졌다...ㅎㅎ

이상적인 구조였다면 버튼 그룹만 따로 다시 컴포넌트화 하여 ButtonGrp.tsx 같은 것을 만들어 

props로 다시 타입을 내려준다면 버튼 그룹에서 버튼만 관리 할 수도 있을 것이다.

추후 수정이나 유지보수를 위해서는 그룹을 따로 분리하는 것이 더 편리할 것 같다.
