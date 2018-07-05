#JDK注册表访问权限#
##问题描述##
测试bubbo接口时，启动报如下的告警信息：

	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences <init>
	WARNING: Could not open/create prefs root node Software\JavaSoft\Prefs at root 0x80000002. Windows RegCreateKeyEx(...) returned error code 5.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	WARNING: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	WARNING: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:14 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:16 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.
	七月 05, 2018 2:00:17 下午 java.util.prefs.WindowsPreferences WindowsRegOpenKey1
	警告: Trying to recreate Windows registry node Software\JavaSoft\Prefs at root 0x80000002.
	七月 05, 2018 2:00:17 下午 java.util.prefs.WindowsPreferences openKey
	警告: Could not open windows registry node Software\JavaSoft\Prefs at root 0x80000002. Windows RegOpenKey(...) returned error code 2.

##问题分析##
告警信息描述的很清晰，就是没有访问权限。
win+R键打开运行窗口，输入：regedit
依次查看HKEY_LOCAL_MACHINE\SOFTWARE发现路径下并没有JavaSoft目录

##问题解决##
解决办法一：
	
	忽略告警信息，因为此告警信息并不会影响程序正常启动。

解决办法二：

	重新安装一个非绿色版的JDK，这样就会创建对应的注册表信息。
