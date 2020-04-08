关于navigation里面传递回调函数
例子：

    _onPressDropDown = () => {
    const { navigation } = this.props;
    navigation.navigate('ChooseCountryCode', {
    onPressCountryCodeItem: (value) => {
    this.setState({ countryCode:  value });
    },
    });
    }

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzM2MDUzNjk1XX0=
-->