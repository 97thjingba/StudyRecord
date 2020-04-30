```js
await console.log('api版本:', DeviceInfo.getAPILevel());
        await console.log('品牌:', DeviceInfo.getBrand());
        await console.log('当前应用名称:', DeviceInfo.getApplicationName());
        await console.log('应用编译版本号:', DeviceInfo.getBuildNumber());
        await console.log('获取应用程序包标识符:', DeviceInfo.getBundleId());
        await console.log('运营商名称:', DeviceInfo.getCarrier());
        await console.log('设备所处国家:', DeviceInfo.getDeviceCountry());
        await console.log('设备ID:', DeviceInfo.getDeviceId());
        await console.log('设备地区:', DeviceInfo.getDeviceLocale());
        await console.log('设备名称:', DeviceInfo.getDeviceName());
        await console.log('获取应用初始安装时间:', DeviceInfo.getFirstInstallTime());
        await console.log('设备字体大小:', DeviceInfo.getFontScale());
        await console.log('剩余存储容量(字节):', DeviceInfo.getFreeDiskStorage());
        await DeviceInfo.getIPAddress().then(res => {
            console.log('设备当前网络地址IP:', res);
        });
        await console.log('应用程序实例ID:', DeviceInfo.getInstanceID());
        await console.log('获取应用上次更新时间:', DeviceInfo.getLastUpdateTime());
        await DeviceInfo.getMACAddress().then(res => {
            console.log('网络适配器MAC地址:', res);
        });
        await console.log('设备制造商:', DeviceInfo.getManufacturer());
        await console.log('获取JVM试图使用的最大内存量(字节):', DeviceInfo.getMaxMemory());
        await console.log('获取设备模式:', DeviceInfo.getModel());
        await console.log('获取电话号码:', DeviceInfo.getPhoneNumber());
        await console.log('获取应用程序可读版本:', DeviceInfo.getReadableVersion());
        await console.log('设备唯一序列号:', DeviceInfo.getSerialNumber());
        await console.log('获取系统名称:', DeviceInfo.getSystemName());
        await console.log('获取系统版本:', DeviceInfo.getSystemVersion());
        await console.log('系统时区:', DeviceInfo.getTimezone());
        await console.log('完整磁盘空间大小(字节):', DeviceInfo.getTotalDiskCapacity());
        await console.log('设备总内存(字节):', DeviceInfo.getTotalMemory());
        await console.log('设备唯一ID:', DeviceInfo.getUniqueID());
        await console.log('设备用户代理:', DeviceInfo.getUserAgent());
        await console.log('设备版本:', DeviceInfo.getVersion());
        await console.log('用户偏好是否设置为24小时格式:', DeviceInfo.is24Hour());
        await console.log('程序是否允许在模拟器中:', DeviceInfo.isEmulator());
        await console.log('是否是平板电脑:', DeviceInfo.isTablet());
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1MDg2MDExMl19
-->