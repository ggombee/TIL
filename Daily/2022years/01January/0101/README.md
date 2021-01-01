# RN Type에 따른 스타일 변화주기

```
const IMAGE_PROPS = {
  [SOCIAL_TYPE.APPLE]: {
    source: assets.social_apple,
    style: {width: 21 / 2, height: 25 / 2},
  },
  [SOCIAL_TYPE.NAVER]: {
    source: assets.social_naver,
    style: {width: 21 / 2, height: 19 / 2},
  },
  [SOCIAL_TYPE.KAKAO]: {
    source: assets.social_kakao,
    style: {width: 26 / 2, height: 24 / 2},
  },
  [SOCIAL_TYPE.GOOGLE]: {
    source: assets.social_google,
    style: {width: 23 / 2, height: 23 / 2},
  },
};
```

위와같이 미리 정의해둔 상수를 통해 스타일을 따로 지정해줄수 있다.

```
const More = () => {
  const {inset, height, heightWithPadding} = usePageHeaderPadding();
  const {principal} = useSelector(s => s.auth, shallowEqual);
  const dispatch = useDispatch();
  const navigation = useNavigation();

  const scrollY = useSharedValue(0);
  const scrollHandler = useAnimatedScrollHandler(event => {
    'worklet';
    scrollY.value = event.contentOffset.y;
  }, []);

  const handleLogout = async () => {
    if (!(await basicConfirm('', '정말 로그아웃하시겠습니까?'))) return;

    await AsyncStorage.removeItem(TOKEN_STORAGE_NAME);
    dispatch(clearPrincipal());
    navigation.navigate('HomeIndex');
  };

  const [receivePush, setReceivePush] = useState(false);

  return (
    <View style={{flex: 1, backgroundColor: colors.background}}>
      <PageHeader scrollY={scrollY}>더보기</PageHeader>
      <Animated.ScrollView
        scrollEventThrottle={16}
        onScroll={scrollHandler}
        contentContainerStyle={{
          paddingTop: heightWithPadding,
          paddingBottom: inset.bottom + 80,
        }}
        scrollIndicatorInsets={{top: height - inset.top}}>
        <View style={styles.profileContainer}>
          <View style={styles.profileImageCover}>
            <Image
              style={styles.profileImage}
              resizeMode={'contain'}
              source={assets.profile}
            />
          </View>
          <View style={styles.typoCover}>
            <Text style={styles.user}>{principal?.nickname}</Text>
            <View style={styles.iconContainer}>
              {/* 타입에 따른 스타일 변화 */}
              <View style={[styles.iconImage, styles[principal?.grant_type]]}>
                <Image {...IMAGE_PROPS[principal?.grant_type]} />
              </View>
              <Text style={styles.email}>{principal?.email}</Text>
            </View>
          </View>
        </View>

        <View style={styles.menuContainer}>
          <TouchableOpacity style={styles.menuItem}>
            <Text style={styles.menuText}>버전정보</Text>
            <Text style={styles.versionText}>v 1.0.0</Text>
          </TouchableOpacity>
          <View style={styles.line} />
        </View>
        <View style={{paddingBottom: 30, paddingTop: 10}}>
          <Copyright />
        </View>
      </Animated.ScrollView>
    </View>
  );
};

export default More;
```
