# Controlling Hyper-V on and off

IMO many guides ([1][1], [2][1], [3][1]) on Hyper-V based technologies emphasize enabling a Windows feature using `dism.exe /enable-feature` or `Enable-WindowsOptionalFeature`.

It is often omitted that `hypervisorlaunchtype` option also needs to be in proper state `auto` otherwise the features may seem enabled but they fail to start.

```
bcdedit /set hypervisorlaunchtype auto
```

Similarly

```
bcdedit /set hypervisorlaunchtype off
```

can help to persuade Hyper-V to release CPU for other virtualization tool like VirtuaBox.
 
[1]: https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-enabling-hyper-v-for-use-on-windows-10/ba-p/267945
[2]: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/reference/hyper-v-requirements
[3]: https://docs.microsoft.com/en-us/windows/wsl/install-win10