# RN footer component

```
footer: {
    position: 'absolute',
    bottom: 0,
    height: 80,
    width: '100%',
    backgroundColor: colors.white,
    justifyContent: 'space-between',
    flexDirection: 'row',
  },
  footerItem: {
    paddingHorizontal: 20,
    paddingVertical: 25,
    flexDirection: 'row',
  },
  footerIconCover: {
    width: 18,
    height: 18,
    borderRadius: 18 / 2,
    backgroundColor: colors.white,
  },

  footerText: {
    marginLeft: 8,
    fontSize: 14,
    fontWeight: 'normal',
    fontStyle: 'normal',
    lineHeight: 15,
    letterSpacing: -0.35,
    textAlign: 'left',
    color: colors.brownGrey1,
  },
```

```
</Animated.ScrollView>
      <View style={styles.footer}>
        <TouchableOpacity
          onPress={() => alert('준비중입니다.')}
          activeOpacity={1}
          style={styles.footerItem}>
          <View style={styles.footerIconCover}>
            <Image
              style={{width: 15, height: 17}}
              resizeMode={'contain'}
              source={assets.magazine_share}
            />
          </View>
          <Text style={styles.footerText}>공유하기</Text>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => alert('준비중입니다.')}
          activeOpacity={1}
          style={styles.footerItem}>
          <View style={styles.footerIconCover}>
            <Image
              style={{width: 18, height: 18}}
              source={assets.magazine_plus}
              resizeMode={'contain'}
            />
          </View>
          <Text style={styles.footerText}>매거진담기</Text>
        </TouchableOpacity>
      </View>
```
