# Arena

#define zwart1 50
#define zwart2 55
#define kwartdraai OnRev(OUT_A,40); OnFwd(OUT_C,40); Wait(450);
#define vooruit50 OnRev(OUT_AC,50);
#define lijnvolgerS1 OnRev(OUT_A,50); OnRev(OUT_C,50); if(SENSOR_1 <= zwart1) { OnFwd(OUT_A,50); OnRev(OUT_C,50); }
#define lijnvolgerS2 if(SENSOR_2 <= zwart2) { OnFwd(OUT_C,50); OnRev(OUT_A,50); }
#define beide_wit if(SENSOR_1 >= zwart1 && SENSOR_2 >= zwart2) { OnRev(OUT_AC,50); }
