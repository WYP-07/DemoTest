# PID算法

```c
//定义结构体
typedef struct 
{
    float SetSpeed;         //定义设定值   
    float ActualSpeed;      //定义实际值
    float err;              //定义偏差值
    float err_last;         //定义上一个偏差值
    float Kp,Ki,Kd;         //定义比例、积分、微分系数
    float voltage;          //定义电压值（控制执行器的变量）
    float integral;         //定义积分值
}pid_variable;

pid_variable Pid;			//结构体变量

//初始化
void PID_init(void)
{
    Pid.SetSpeed=0.0;
    Pid.ActualSpeed=0.0;
    Pid.err=0.0;
    Pid.err_last=0.0;
    Pid.voltage=0.0;
    Pid.integral=0.0;
    Pid.Kp=0.2;
    Pid.Ki=0.015;
    Pid.Kd=0.2;
    printf("PID_init end \n");
}

//算法实现
float PID_realize(float speed)
{
    Pid.SetSpeed = speed;
    Pid.err = Pid.SetSpeed-Pid.ActualSpeed;
    Pid.integral += Pid.err;
    Pid.voltage = Pid.Kp * Pid.err + Pid.Ki * Pid.integral + Pid.Kd * (Pid.err - Pid.err_last);
    Pid.err_last = Pid.err;
    Pid.ActualSpeed = Pid.voltage*1.0f;
    
    return Pid.ActualSpeed;
}
```

