# frida-gum-fix
trying-to-avoid-rwxp-by-modifying-sourcecode
目前仍有一部分rwxp，如一部分libart.so,尚未查明在何处生成。libc.so的rwxp应该已经去除
```log
windows_x86_64:/ # cat /proc/5077/maps | grep rwxp
6ff53000-6ff54000 rwxp 00094000 08:00 1344                               /system/framework/x86_64/boot.oat
741d45199000-741d451a0000 rwxp 00000000 00:00 0
741dba37d000-741dba37e000 rwxp 0017d000 07:1c 85                         /apex/com.android.art/lib64/libart.so
741dba60c000-741dba60d000 rwxp 0040c000 07:1c 85                         /apex/com.android.art/lib64/libart.so
741dba7fc000-741dba7fd000 rwxp 005fc000 07:1c 85                         /apex/com.android.art/lib64/libart.so
741dba7fe000-741dba7ff000 rwxp 005fe000 07:1c 85                         /apex/com.android.art/lib64/libart.so
742059e61000-742059e71000 rwxp 00000000 00:00 0
74205bafc000-74205bb0e000 rwxp 00000000 00:00 0
742065300000-742065307000 rwxp 00000000 00:00 0
7420657d3000-7420657d4000 rwxp 00000000 00:00 0
74206c27e000-74206c27f000 rwxp 00000000 00:00 0
```
打印的日志输出
```shell
--------- beginning of main
--------- beginning of system
2025-01-27 18:56:15.831   370-5793  FridaGum                system_server                        D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:15.831   370-5793  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e75ab3c000
2025-01-27 18:56:15.831   370-5793  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e75aae3000
2025-01-27 18:56:15.831   370-5793  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e75aaf1000
2025-01-27 18:56:15.831   370-5793  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e75ab46000
2025-01-27 18:56:15.896   370-5797  FridaGum                system_server                        D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:15.896   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9bf1000
2025-01-27 18:56:15.965   370-5797  FridaGum                system_server                        D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:15.965   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9bf2000
2025-01-27 18:56:15.965   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9d7a000
2025-01-27 18:56:15.965   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9d79000
2025-01-27 18:56:15.965   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9d7b000
2025-01-27 18:56:15.966   370-5797  FridaGum                system_server                        D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:15.966   370-5797  FridaGum                system_server                        D  Revoking RWX permissions for page: 0x74e4b9cb3000
2025-01-27 18:56:16.188   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:16.188   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75ab3c000
2025-01-27 18:56:16.188   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75aae3000
2025-01-27 18:56:16.188   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75aaf1000
2025-01-27 18:56:16.188   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75ab46000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75aadf000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75ab3a000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75ab53000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75aae5000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75aae7000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e75eab6000
2025-01-27 18:56:16.203   176-5806  FridaGum                zygote64                             D  Revoking RWX permissions for page: 0x74e767d6d000
2025-01-27 18:56:16.318   178-5816  FridaGum                zygote                               D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:16.318   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xeddda000
2025-01-27 18:56:16.318   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xeddcb000
2025-01-27 18:56:16.318   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xede2f000
2025-01-27 18:56:16.318   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xede25000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions after hook is applied.
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xecee0000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xede22000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xeddaf000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xeddcd000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xeddcf000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xf1f47000
2025-01-27 18:56:16.345   178-5816  FridaGum                zygote                               D  Revoking RWX permissions for page: 0xede3e000
2025-01-27 18:57:23.972  5313-5992  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions after hook is applied.
2025-01-27 18:57:23.972  5313-5992  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e75ab3c000
2025-01-27 18:57:23.972  5313-5992  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e75aae3000
2025-01-27 18:57:23.972  5313-5992  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e75aaf1000
2025-01-27 18:57:23.972  5313-5992  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e75ab46000
2025-01-27 18:57:24.269  5313-5996  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions after hook is applied.
2025-01-27 18:57:24.269  5313-5996  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e4b9bf1000
2025-01-27 18:57:24.279  5313-5996  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions after hook is applied.
2025-01-27 18:57:24.279  5313-5996  FridaGum                com.zj.wuaipojie                     D  Revoking RWX permissions for page: 0x74e4b9bf1000
```