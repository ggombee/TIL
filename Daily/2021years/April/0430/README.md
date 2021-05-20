```jsx

function BuyerBtn(): React.ReactElement {

  switch (statusCd) {
    //판매대기 (C2C, B2C)
    case '00':
      return (
        <button
          type="button"
          className={cx('btn', 'btn-main')}
          onClick={() => handleClickMove('1')}
        >
          문의하기
        </button>
      );
    // 거래중 (C2C)
    case '02':
      return (
        <>
          {/*구매자이고 배송완료 경우 노출*/}
          {myUserType === 'B' && ordSttsCd === '03' ? (
            <>
              <button
                type="button"
                className={cx('btn', 'btn-default')}
                onClick={() => handleClickMove('1')}
              >
                문의하기
              </button>
              <button
                type="button"
                className={cx('btn', 'btn-main')}
                onClick={() => handleClickMove('3')}
              >
                구매확정
              </button>
            </>
          ) : (
            <button
              type="button"
              className={cx('btn', 'btn-main')}
              onClick={() => handleClickMove('1')}
            >
              문의하기
            </button>
          )}
        </>
      );
    //판매중 (C2C, B2C)
    case '01':
      return (
        <>
          {myUserType === 'B' ? (
            //재고가 있는 상품의 구매자일때
            <>
              {!reviewExist ? (
                //리뷰가 없고
                <>
                  {ordSttsCd === '08' && ordFinDayCnt <= 3 ? (
                    // 구매확정 상태일경우 구매확정 후 3일이 안지난경우
                    <>
                      <button
                        type="button"
                        className={cx('btn', 'btn-default')}
                        onClick={() => handleClickMove('1')}
                      >
                        문의하기
                      </button>
                      <button
                        type="button"
                        className={cx('btn', 'btn-main')}
                        onClick={() => handleClickMove('2')}
                      >
                        거래후기 쓰기
                      </button>
                    </>
                  ) : (
                    //구매확정 후 3일이 지난경우
                    <>
                      {ordSttsCd === '03' ? (
                        // 리뷰 O , B2C 배송완료 상태일경우
                        <>
                          <button
                            type="button"
                            className={cx('btn', 'btn-default')}
                            onClick={() => handleClickMove('1')}
                          >
                            문의하기
                          </button>
                          <button
                            type="button"
                            className={cx('btn', 'btn-main')}
                            onClick={() => handleClickMove('3')}
                          >
                            구매확정
                          </button>
                        </>
                      ) : (
                        // 리뷰 O || 판매완료, 구매확정후 3일후 상태, 재고 O
                        <>
                          {buyable ? (
                            <>
                              <button
                                type="button"
                                className={cx('btn', 'btn-default')}
                                onClick={() => handleClickMove('1')}
                              >
                                문의하기
                              </button>
                              <button
                                type="button"
                                className={cx('btn', 'btn-main')}
                                onClick={() => handleClickMove('0')}
                              >
                                추가구매
                              </button>
                            </>
                          ) : (
                            // 리뷰 O || 판매완료, 구매확정후 3일후 상태, 재고 X
                            <>
                              <button
                                type="button"
                                className={cx('btn', 'btn-main')}
                                onClick={() => handleClickMove('1')}
                              >
                                문의하기
                              </button>
                            </>
                          )}
                        </>
                      )}
                    </>
                  )}
                </>
              ) : (
                //리뷰가 있고 구매확정 상태일경우
                <>
                  {buyable ? (
                    <>
                      <button
                        type="button"
                        className={cx('btn', 'btn-default')}
                        onClick={() => handleClickMove('1')}
                      >
                        문의하기
                      </button>
                      <button
                        type="button"
                        className={cx('btn', 'btn-main')}
                        onClick={() => handleClickMove('0')}
                      >
                        추가구매
                      </button>
                    </>
                  ) : (
                    <>
                      <button
                        type="button"
                        className={cx('btn', 'btn-main')}
                        onClick={() => handleClickMove('1')}
                      >
                        문의하기
                      </button>
                    </>
                  )}
                </>
              )}
            </>
          ) : (
            //일반사용자일때
            <>
              {buyable ? (
                <>
                  <button
                    type="button"
                    className={cx('btn', 'btn-default')}
                    onClick={() => handleClickMove('1')}
                  >
                    문의하기
                  </button>
                  <button
                    type="button"
                    className={cx('btn', 'btn-main')}
                    onClick={() => handleClickMove('0')}
                  >
                    결제하기
                  </button>
                </>
              ) : (
                <>
                  <button
                    type="button"
                    className={cx('btn', 'btn-main')}
                    onClick={() => handleClickMove('1')}
                  >
                    문의하기
                  </button>
                </>
              )}
            </>
          )}
        </>
      );
    //판매완료 (C2C, B2C)
    case '03':
      return (
        //재고 없음 (있다면 판매등록 상태임)
        <>
          {myUserType === 'B' ? (
            //구매자일때
            <>
              {!reviewExist && ordSttsCd === '08' ? (
                //리뷰가 없고 구매확정 상태일경우
                <>
                  {ordFinDayCnt <= 3 ? (
                    //구매확정 후 3일이 안지난경우
                    <>
                      <button
                        type="button"
                        className={cx('btn', 'btn-default')}
                        onClick={() => handleClickMove('1')}
                      >
                        문의하기
                      </button>
                      <button
                        type="button"
                        className={cx('btn', 'btn-main')}
                        onClick={() => handleClickMove('2')}
                      >
                        거래후기 쓰기
                      </button>
                    </>
                  ) : (
                    //구매확정 후 3일이 지난경우
                    <button
                      type="button"
                      className={cx('btn', 'btn-main')}
                      onClick={() => handleClickMove('1')}
                    >
                      문의하기
                    </button>
                  )}
                </>
              ) : (
                //리뷰가 있고 구매확정 상태일경우
                <button
                  type="button"
                  className={cx('btn', 'btn-main')}
                  onClick={() => handleClickMove('1')}
                >
                  문의하기
                </button>
              )}
            </>
          ) : (
            //일반사용자일때
            <>
              <button
                type="button"
                className={cx('btn', 'btn-main')}
                onClick={() => handleClickMove('1')}
              >
                문의하기
              </button>
            </>
          )}
        </>
      );
    default:
      return <></>;
  }
}

export default BuyerBtn;
```

Button.tsx

```jsx
import React, { useEffect, useState } from 'react';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_goodsdetail.module.scss';

const cx = classNames.bind(styles);

interface Props {
  type: string;
  onClickMove: (string) => void;
  funcNo: string;
  funcNm: string;
  funcNo2?: string;
  funcNm2?: string;
}

function Button(props: Props): React.ReactElement {
  const [moveNo, setMoveNo] = useState('');
  const [moveNo2, setMoveNo2] = useState('');

  const { funcNo, type, onClickMove, funcNm } = props;
  const funcNo2 = props.funcNo2 ? props.funcNo2 : '';
  const funcNm2 = props.funcNm2 ? props.funcNm2 : '';

  useEffect(() => {
    type && (setMoveNo(funcNo), setMoveNo2(''));
  }, [type, funcNo, funcNo2]);

  return (
    <>
      {type === 'single' ? (
        <>
          <button
            type="button"
            className={cx('btn', 'btn-main')}
            onClick={() => onClickMove(moveNo)}
          >
            {funcNm}
          </button>
        </>
      ) : (
        <>
          <button
            type="button"
            className={cx('btn', 'btn-default')}
            onClick={() => onClickMove(moveNo)}
          >
            {funcNm}
          </button>
          <button
            type="button"
            className={cx('btn', 'btn-main')}
            onClick={() => onClickMove(moveNo2)}
          >
            {funcNm2}
          </button>
        </>
      )}
    </>
  );
}

export default Button;
```

```jsx

function BuyerBtn(): React.ReactElement {

  // 버튼 클릭 시 이동
  const handleClickMove = type => {
    if (type === '0') {
      // 결제하기
      history.push({
        pathname: '/payments',
        search: `?saleNo=${saleNo}&goodsNo=${goodsNo}`,
      });
    } else if (type === '1') {
      // 문의하기
      if (myUserBlockYn === 'Y') {
        // 차단된 사용자일경우
        dispatch(isAlertPop(true));
        dispatch(getPopText('판매자의 요청에 의해 참여가 제한되었습니다.'));
      } else if (myUserBlockYn === 'N') {
        history.push({
          pathname: '/chat/detail',
          search: `?saleNo=${saleNo}&goodsNo=${goodsNo}`,
        });
      }
    } else if (type === '2') {
      // 거래후기 쓰기
      if (myUserBlockYn === 'Y') {
        // 차단된 사용자일경우
        dispatch(isAlertPop(true));
        dispatch(getPopText('판매자의 요청에 의해 참여가 제한되었습니다.'));
      } else if (myUserBlockYn === 'N') {
        history.push({
          pathname: '/review/add',
          search: `?saleNo=${saleNo}&ordNo=${ordNo}&from=detail`,
        });
      }
    } else if (type === '3') {
      //중복클릭방지
      if (disabled) return;
      setDisabled(true);
      // 리뷰 구매내역 등록
      api
        .post(
          '/review/orders',
          {
            orderId: goodsInfo.ordNo,
            orderUserId: goodsInfo.buyerId,
            orderDate: goodsInfo.ordDtime,
            goodsList: [
              {
                goodsId: goodsInfo.goodsNo,
                goodsPrice: goodsInfo.saleAmt,
                goodsRealPrice: goodsInfo.saleAmt,
                goodsName: goodsInfo.goodsNm,
              },
            ],
          },
        )
        .then(() => {
          api
            .get('/goods/buy/confirm', {
              params: {
                ordNo: ordNo,
              },
            })
            .then(() => {
              // 구매확정팝업
              dispatch(openReviewPop(true));
            })
            .catch(error => {
              alert(error.response.data.message);
            });
        })
        .catch(error => {
          alert(error.response.data.message);
        })
        .finally(() => setDisabled(false));
    }
  };

  switch (statusCd) {
    //판매대기 (C2C, B2C)
    case '00':
      return (
        <Button
          type="single"
          onClickMove={handleClickMove}
          funcNo="1"
          funcNm="문의하기"
        />
      );
    // 거래중 (C2C)
    case '02':
      return (
        <>
          {/*구매자이고 배송완료 경우 노출*/}
          {myUserType === 'B' && ordSttsCd === '03' ? (
            <>
              <Button
                type="double"
                onClickMove={handleClickMove}
                funcNo="1"
                funcNm="문의하기"
                funcNo2="3"
                funcNm2="구매확정"
              />
            </>
          ) : (
            <Button
              type="single"
              onClickMove={handleClickMove}
              funcNo="1"
              funcNm="문의하기"
            />
          )}
        </>
      );
    //판매중 (C2C, B2C)
    case '01':
      return (
        <>
          {myUserType === 'B' ? (
            //재고가 있는 상품의 구매자일때
            <>
              {!reviewExist ? (
                //리뷰가 없고
                <>
                  {ordSttsCd === '08' && ordFinDayCnt <= 3 ? (
                    // 구매확정 상태일경우 구매확정 후 3일이 안지난경우
                    <>
                      <Button
                        type="double"
                        onClickMove={handleClickMove}
                        funcNo="1"
                        funcNm="문의하기"
                        funcNo2="2"
                        funcNm2="거래후기 쓰기"
                      />
                    </>
                  ) : (
                    //구매확정 후 3일이 지난경우
                    <>
                      {ordSttsCd === '03' ? (
                        // 리뷰 O , B2C 배송완료 상태일경우
                        <>
                          <Button
                            type="double"
                            onClickMove={handleClickMove}
                            funcNo="1"
                            funcNm="문의하기"
                            funcNo2="3"
                            funcNm2="구매확정"
                          />
                        </>
                      ) : (
                        // 리뷰 O || 판매완료, 구매확정후 3일후 상태, 재고 O
                        <>
                          {buyable ? (
                            <>
                              <Button
                                type="double"
                                onClickMove={handleClickMove}
                                funcNo="1"
                                funcNm="문의하기"
                                funcNo2="0"
                                funcNm2="추가구매"
                              />
                            </>
                          ) : (
                            // 리뷰 O || 판매완료, 구매확정후 3일후 상태, 재고 X
                            <>
                              <Button
                                type="single"
                                onClickMove={handleClickMove}
                                funcNo="1"
                                funcNm="문의하기"
                              />
                            </>
                          )}
                        </>
                      )}
                    </>
                  )}
                </>
              ) : (
                //리뷰가 있고 구매확정 상태일경우
                <>
                  {buyable ? (
                    <>
                      <Button
                        type="double"
                        onClickMove={handleClickMove}
                        funcNo="1"
                        funcNm="문의하기"
                        funcNo2="0"
                        funcNm2="추가구매"
                      />
                    </>
                  ) : (
                    <>
                      <Button
                        type="single"
                        onClickMove={handleClickMove}
                        funcNo="1"
                        funcNm="문의하기"
                      />
                    </>
                  )}
                </>
              )}
            </>
          ) : (
            //일반사용자일때
            <>
              {buyable ? (
                <>
                  <Button
                    type="double"
                    onClickMove={handleClickMove}
                    funcNo="1"
                    funcNm="문의하기"
                    funcNo2="0"
                    funcNm2="결제하기"
                  />
                </>
              ) : (
                <>
                  <Button
                    type="single"
                    onClickMove={handleClickMove}
                    funcNo="1"
                    funcNm="문의하기"
                  />
                </>
              )}
            </>
          )}
        </>
      );
    //판매완료 (C2C, B2C)
    case '03':
      return (
        //재고 없음 (있다면 판매등록 상태임)
        <>
          {myUserType === 'B' ? (
            //구매자일때
            <>
              {!reviewExist && ordSttsCd === '08' ? (
                //리뷰가 없고 구매확정 상태일경우
                <>
                  {ordFinDayCnt <= 3 ? (
                    //구매확정 후 3일이 안지난경우
                    <>
                      <Button
                        type="double"
                        onClickMove={handleClickMove}
                        funcNo="1"
                        funcNm="문의하기"
                        funcNo2="2"
                        funcNm2="거래후기"
                      />
                    </>
                  ) : (
                    //구매확정 후 3일이 지난경우
                    <Button
                      type="single"
                      onClickMove={handleClickMove}
                      funcNo="1"
                      funcNm="문의하기"
                    />
                  )}
                </>
              ) : (
                //리뷰가 있고 구매확정 상태일경우
                <Button
                  type="single"
                  onClickMove={handleClickMove}
                  funcNo="1"
                  funcNm="문의하기"
                />
              )}
            </>
          ) : (
            //일반사용자일때
            <>
              <Button
                type="single"
                onClickMove={handleClickMove}
                funcNo="1"
                funcNm="문의하기"
              />
            </>
          )}
        </>
      );
    default:
      return <></>;
  }
}

export default BuyerBtn;
```
