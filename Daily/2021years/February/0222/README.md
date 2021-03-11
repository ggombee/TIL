## 코드 정리 해야됨

import 경로지정 말고 각 폴더마다 index파일에 export를 해서 한꺼번에 import 한다 

```jsx
import React from 'react';
import { Switch, Route } from 'react-router-dom';
import Main from 'src/containers/Main';
import Intro from 'src/containers/App/Intro';
import Search from 'src/containers/Search';
import GoodsList from 'src/containers/MainGoodsList';
import GoodsDetail from 'src/containers/GoodsDetail';
import Address from 'src/containers/MyAddress';
import AddAddress from 'src/containers/MyAddress/AddAddress';
import MyProfile from 'src/containers/MyProfile';
import Sell from 'src/containers/Sell';
import Goods from 'src/containers/Sell/SellGoods';
import Price from 'src/containers/Sell/SellPrice';
import Description from 'src/containers/Sell/SellDescription';
import Ledger from 'src/containers/Ledger';
import MyProduct from 'src/containers/MyProduct';
import MyTrading from 'src/containers/MyTrading';
import Chat from 'src/containers/Chat';
import Myorder from 'src/containers/MyOrder';
import AuthLogin from 'src/containers/AuthLogin';
import DeliverySelct from 'src/containers/MyOrder/DeliverySelect';
import DeliveryNum from 'src/containers/MyOrder/DeliveryNum';
import ConvenienceService from 'src/containers/MyOrder/ConvenienceService';
import AuthResister from 'src/containers/AuthResister';

//앱 기본 화면
function BasePage(): React.ReactElement {
  return (
    <>
      <Switch>
        <Route exact path="/" component={Main} />
        <Route exact path="/intro" component={Intro} />
        <Route exact path="/search" component={Search} />
        <Route exact path="/sell" component={Sell} />
        <Route exact path="/myprofile" component={MyProfile} />
        <Route exact path="/sell/goods" component={Goods} />
        <Route exact path="/sell/goods/price" component={Price} />
        <Route
          exact
          path="/sell/goods/price/description"
          component={Description}
        />
        <Route exact path="/goodslist" component={GoodsList} />
        <Route path="/goodsdetail" component={GoodsDetail} />
        <Route exact path="/address" component={Address} />
        <Route exact path="/address/add" component={AddAddress} />
        <Route exact path="/ledger" component={Ledger} />
        <Route exact path="/myproduct" component={MyProduct} />
        <Route exact path="/mytrading" component={MyTrading} />
        <Route exact path="/chat" component={Chat} />
        <Route exact path="/auth/login" component={AuthLogin} />
        <Route exact path="/auth/resister" component={AuthResister} />
        <Route exact path="/myorder" component={Myorder} />
        <Route exact path="/login" component={AuthLogin} />
        <Route exact path="/myorder/deliveryselcet" component={DeliverySelct} />
        <Route
          exact
          path="/myorder/deli/conve"
          component={ConvenienceService}
        />
        <Route exact path="/myorder/deli/deliverynum" component={DeliveryNum} />
      </Switch>
    </>
  );
}

export default BasePage;
```

```jsx
import React, { useCallback, useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { useHistory } from 'react-router-dom';

import 'src/styles/scss/pages/goodsdetail.scss';
import { selectGoodsInfo } from '../../stores/GoodsDetail/actions';
import { GoodsData } from '../../stores/GoodsDetail/__mocksData__/mockData';
import { RootState } from '../../stores/rootReducer';

import GoodsImageBanner from './GoodsImageBanner';
import GoodsInfoCard from './GoodsInfoCard';

function GoodsDetail(): React.ReactElement {
  const dispatch = useDispatch();
  const history = useHistory();

  const { goodsInfo } = useSelector((state: RootState) => {
    return {
      goodsInfo: state.goodsdetail.goodsInfo,
    };
  });

  const getGoodsInfo = useCallback(() => {
    dispatch(selectGoodsInfo(GoodsData));
  }, [dispatch]);

  const goodsImgList = goodsInfo.goodsImgList;

  useEffect(() => {
    getGoodsInfo();
  }, [getGoodsInfo]);

  const handleClickMove = () => {
    history.goBack();
  };

  return (
    <div className="de-se-wrap detail-box">
      {goodsInfo && (
        <>
          {/*헤더 영역*/}
          <header className="header-sec">
            <button
              type="button"
              className="btn-back"
              onClick={handleClickMove}
            >
              <i className="icon icon-back" />
            </button>
            <button type="button" className="btn-share">
              <i className="icon icon-share" />
            </button>
          </header>
          {/*상품이미지 배너 영역*/}
          <GoodsImageBanner imgList={goodsImgList} />
          {/*스크롤 컨텐츠 영역*/}
          <GoodsInfoCard {...goodsInfo} />
        </>
      )}
    </div>
  );
}

export default GoodsDetail;
```
