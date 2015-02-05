# Arena

#define zwart1 50
#define zwart2 55
#define kwartdraai OnRev(OUT_A,40); OnFwd(OUT_C,40); Wait(450);
#define vooruit50 OnRev(OUT_AC,50);
#define lijnvolgerS1 OnRev(OUT_A,50); OnRev(OUT_C,50); if(SENSOR_1 <= zwart1) { OnFwd(OUT_A,50); OnRev(OUT_C,50); }
#define lijnvolgerS2 if(SENSOR_2 <= zwart2) { OnFwd(OUT_C,50); OnRev(OUT_A,50); }
#define beide_wit if(SENSOR_1 >= zwart1 && SENSOR_2 >= zwart2) { OnRev(OUT_AC,50); }
#define kwartdraai3 OnRev(OUT_C,40); OnRev(OUT_A,80); Wait(1200);
#define achteruit OnFwd(OUT_AC,50); Wait(500);

task lijnvolger();

task main()
{
     SetSensorLight(S1);
     SetSensorLight(S2);
     SetSensorLowspeed(S3);
     SetSensorLowspeed(S4);

     achteruit
     kwartdraai
     Off(OUT_AC);
     vooruit50
     if(SENSOR_4 <= 20)
     {
                 kwartdraai3
                 vooruit50
     }
     if(SENSOR_4 >= 20)
     {
                 kwartdraai3
                 vooruit50
     }
     if(SENSOR_1 <= zwart1)
     {
                 Off(OUT_A);
                 OnRev(OUT_C,100);
                 if(SENSOR_2 <= zwart2)
                 {
                             OnFwd(OUT_C,100);
                             OnRev(OUT_A,100);
                             ExitTo(lijnvolger);
                 }
     }
}

task lijnvolger()
{
     vooruit50
}
