## 숫자만 입력...ㅠㅠ 공백,- 입력방지

```jsx
import React, { useEffect, useState } from 'react';
import SubHeader from '../../component/Common/SubHeader';

import * as classNames from 'classnames/bind';
import styles from 'src/styles/scss/modules/_saferedo.module.scss';
const cx = classNames.bind(styles);

function SafereDo(): React.ReactElement {
  const [isActive, setIsActive] = useState(false);
  const [goodsNm, setGoodsNm] = useState('');
  const [goodsCd, setGoodsCd] = useState(0);
  const [goodsInfo, setGoodsInfo] = useState({
    goodsNm: '',
    goodsCd: 0,
  });
  const [warn, setWarn] = useState(false);

  const handleChange = e => {
    const str_space = /\s/;
    const str_hyphen = /-/;
    if (e.target.id === 'name') {
      e.target.value.length < 31
        ? (setGoodsNm(e.target.value), setWarn(false))
        : (setWarn(true), setIsActive(false));
    } else if (e.target.id === 'number') {
      // 공백입력방지
      if (str_space.exec(e.target.value)) {
        e.target.value.replace(' ', '');
        setGoodsCd(e.target.value.replace(' ', ''));
      } // - 입력방지
      else if (str_hyphen.exec(e.target.value)) {
        e.target.value.replace('-', '');
        setGoodsCd(e.target.value.replace('-', ''));
      } else {
        setGoodsCd(e.target.value.replace(/[^0-9.]/g, ''));
      }
    }
  };

  const handleClickConfirm = () => {
    console.log('팝업을 열어라');
  };

  useEffect(() => {
    setGoodsInfo({
      goodsNm: goodsNm,
      goodsCd: goodsCd,
    });
  }, [goodsNm, goodsCd]);

  useEffect(() => {
    if (goodsInfo.goodsCd > 0 && goodsInfo.goodsNm.length > 0) {
      setIsActive(true);
    } else {
      setIsActive(false);
    }
  }, [goodsInfo]);

  return (
    <div className={cx('se-sa-wrap')}>
      <SubHeader title="세이프리가 해드려요" />
      <div className={cx('area-body')}>
        <div className={cx('guide-text')}>
          <p className={cx('message')}>
            제품 정보를 입력하시면 <br />
            세이프리가 등록해드려요.
          </p>
        </div>

        <div className={cx('cta-box')}>
          <div className={cx('input-box-wrap', 'mb42')}>
            <span className={cx('label')}>제품 명</span>
            <input
              type="text"
              id="name"
              value={goodsNm}
              onChange={handleChange}
              className={cx('check-input', warn ? 'warn' : '')}
              maxLength={31}
              placeholder="30자 이내로 입력해주세요."
            />
            <p className={cx('warn')}>30자 이내로 작성 해주세요.</p>
          </div>
          <div className={cx('input-box-wrap')}>
            <span className={cx('label')}>제품 일련 번호</span>
            <input
              type="text"
              id="number"
              value={goodsCd === 0 ? '' : goodsCd}
              onChange={handleChange}
              placeholder="(-) 없이 입력해주세요."
            />
          </div>
        </div>
      </div>
      <div className={cx('btn-list', 'bottom-fixed')}>
        <button
          type="button"
          className={cx('btn', 'btn-main', isActive ? '' : 'off')}
          disabled={!isActive}
          onClick={handleClickConfirm}
        >
          등록 신청
        </button>
      </div>
    </div>
  );
}

export default SafereDo;
```
