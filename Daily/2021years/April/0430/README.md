
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
