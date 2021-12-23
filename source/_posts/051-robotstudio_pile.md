---
title: RobotStudio码垛机器人创建过程
date: 2021-02-13 23:59:20
description: 首先导入一个IRB2600机器人，移动夹具的本地坐标原点，使原点位置为顶面中心（与法兰盘连接的部位）。对齐夹爪Smart组件的本地坐标和机器人末端法兰盘的坐标...
categories:
- 机器人
- RobotStudio
tags:
- 实验
- robotstudio
---


### 一、安装夹具
1. 导入一个IRB2600机器人
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231608015-robotstudio-plie-1.png)
2. 移动夹具的本地坐标原点，使原点位置为顶面中心（与法兰盘连接的部位）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231608361-robotstudio-pile-2.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231609484-robotstudio-pile-3.png)
3. 对齐夹爪Smart组件的本地坐标和机器人末端法兰盘的坐标，使夹具的本地坐标与法兰盘的本地坐标重合，为下一步安装夹具做准备。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231609408-robotstudio-pile-4.png)
4. 在布局菜单内，将夹具拖动到IRB2600机器人上，完成夹具的安装
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231609685-robotstudio-pile-5.png)
### 二、创建传送带
1. 导入传送带并设定传送带的位置
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231610899-robotstudio-pile-6.png)
2. 创建码垛用的物体，并将其移动到传送带的起点。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231610645-robotstudio-pile-7.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231610831-robotstudio-pile-8.png)
3. 创建一个Smart组件，用于传送带物体的运动。添加如下组件
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231610947-robotstudio-pile-9.png)
4. 对各个组件进行设置
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231611124-robotstudio-pile-10.png)

![](https://gitee.com/huffiema/pictures/raw/master/image/202112231611916-robotstudio-pile-11.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231611919-robotstudio-pile-12.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231612829-robotstudio-pile-13.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231612841-robotstudio-pile-14.png)

### 三、创建码垛底盘
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231612709-robotstudio-pile-15.png)
### 四、创建机器人系统
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231613609-robotstudio-pile-16.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231613209-robotstudio-pile-17.png)
选项内选择如下选项
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231613116-robotstudio-pile-18.png)

### 五、仿真系统设置
1. 在仿真设定中，将机器人系统后面的框选去除。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231613549-robotstudio-pile-19.png)
2. 运行仿真，使物块到达面传感器处，然后停止仿真，捕捉几个目标点。（后面两个目标点是为了码垛时，物块会有两种拜访姿态，所以使用两个目标点）
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231614390-robotstudio-pile-20.png)
3. 旋转第三个目标点，使其绕Z轴旋转-90度。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231614934-robotstudio-pile-21.png)
4. 为目标点配置参数
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231614719-robotstudio-pile-22.png)
5. 使机器人回到机械原点，然后创建一个空路径，将三个目标点依次拖动到路径中。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231615329-robotstudio-pile-23.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231615980-robotstudio-pile-24.png)
6. 同步到工作站
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231615993-robotstudio-pile-25.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231616848-robotstudio-pile-26.png)
7. 删除之前仿真出来的物块的copy物体。
8. 添加两个信号，一个是到位信号，用于传送带的等待，另一个是夹具信号。添加完成后重启控制器。
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231616755-robotstudio-pile-27.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231616351-robotstudio-pile-28.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231617959-robostudio-pile-29.png)
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231617558-robotstudio-pile-30.png)

9. 打开控制器，可以看到RAPID/T_ROB1下的程序模块，接下来就可以进行程序编写了。
### 程序编写
main程序代码如下
```c
MODULE Module1
	CONST robtarget Target_10:=[[347.037,682.5,875.06],[1,0,0,0],[0,0,0,0],[9E9,9E9,9E9,9E9,9E9,9E9]];
	CONST robtarget Target_20:=[[500,-300,100],[1,0,0,0],[-1,0,-1,0],[9E9,9E9,9E9,9E9,9E9,9E9]];
	CONST robtarget Target_30:=[[500,-300,100],[0,0,0,1],[-1,0,1,0],[9E9,9E9,9E9,9E9,9E9,9E9]];
	VAR num layer:=1;
    VAR num x:=0;
    VAR num z:=0;
    PROC main()
        FOR i FROM 0 TO 20 DO
            SetDO JiaJu0,0;
            MoveJ Offs(Target_10,0,0,200),v500,fine,Tool1;
            WaitDI DaoWei0,1; 
            MoveL Offs(Target_10,0,0,0),v500,fine,Tool1;
            SetDO JiaJu0,1;
            WaitTime 1;
            MoveL Offs(Target_10,0,0,200),v500,fine,Tool1;

            IF layer MOD 2 = 1 THEN
                IF i MOD 5 < 4 and i MOD 5 <> 0 THEN
                    MoveL Offs(Target_30,90+x,-150,300+z),v500,fine,Tool1;
                    MoveL Offs(Target_30,90+x,-150,100+z),v500,fine,Tool1;
                    SetDO JiaJu0,0;
                    WaitTime 1;
                    MoveL Offs(Target_30,90+x,-150,300+z),v500,fine,Tool1;
                    x:=x+210;
                    IF i MOD 5 = 3 THEN
                        x:=0;
                    ENDIF
                ELSE
                    MoveL Offs(Target_20,150+x,-410,300+z),v500,fine,Tool1;
                    MoveL Offs(Target_20,150+x,-410,100+z),v500,fine,Tool1;
                    SetDO JiaJu0,0;
                    WaitTime 1;
                    MoveL Offs(Target_20,150+x,-410,300+z),v500,fine,Tool1;
                    x:=x+300;
                ENDIF
                IF i MOD 5 = 0 THEN
                    layer:=2;
                    x:=0;
                    z:=z+100;
                ENDIF
                
            ELSE
                IF i MOD 5 < 3 THEN
                    MoveL Offs(Target_20,150+x,-100,300+z),v500,fine,Tool1;
                    MoveL Offs(Target_20,150+x,-100,100+z),v500,fine,Tool1;
                    SetDO JiaJu0,0;
                    WaitTime 1;
                    MoveL Offs(Target_20,150+x,-100,300+z),v500,fine,Tool1;
                    x:=x+300;
                    IF i MOD 5 = 2 THEN
                        x:=0;
                    ENDIF
                ELSE
                    MoveL Offs(Target_30,100+x,-350,300+z),v500,fine,Tool1;
                    MoveL Offs(Target_30,100+x,-350,100+z),v500,fine,Tool1;
                    SetDO JiaJu0,0;
                    WaitTime 1;
                    MoveL Offs(Target_30,100+x,-350,300+z),v500,fine,Tool1;
                    x:=x+210;
                ENDIF
                IF i MOD 5 = 0 THEN
                    layer:=1;
                    x:=0;
                    z:=z+100;
                ENDIF
            ENDIF
                
        ENDFOR
        z:=0;
    ENDPROC
ENDMODULE
```

### 仿真测试
1. 将代码同步到工作站
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231617535-robotstudio-pile-31.png)
 2. 删除Path_10路径，只保留main路径
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231617120-robotstudio-pile-32.png)
2. 设置工作站逻辑
![](https://gitee.com/huffiema/pictures/raw/master/image/202112231618997-robotstudio-pile-33.png)
3. 进行仿真