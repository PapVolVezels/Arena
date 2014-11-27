#define zwart1 50
#define zwart2 55
#define motoren OUT_AC
#define kwartdraai1 150                                                         //getest snelheid van 40
#define halvedraai1 100                                                         //getest snelheid van 70
#define heledraai1 300                                                          //getest snelheid van 100
#define kwartdraai2 50                                                          //getest snelheid van 70
#define halvedraai2 300                                                         //getest snelheid van 100
#define heledraai2 1500                                                         //getest snelheid van 100
#define kwartdraai3 400                                                         //getest snelheid van 40,80
#define halvedraai3 1700                                                        //getest snelheid van 40,80
#define heledraai3 4150                                                         //getest snelheid van 40,80

task STEEN_ONTWIJKEN();
task anderekant();
task lijnvolger();

task main()
{
     while(true)
     {
                SetSensorLight(SENSOR_1);
                SetSensorLight(SENSOR_2);

                if(SENSOR_1 <= zwart1)
                {
                            OnFwd(OUT_A,100);
                            OnRev(OUT_C,100);
                }
                if(SENSOR_2 <= zwart2)
                {
                            OnFwd(OUT_C,100);
                            OnRev(OUT_A,100);
                }
                if(SENSOR_1 >= zwart1 && SENSOR_2 >= zwart2)
                {
                            Off(OUT_C);
                }
                if(SENSOR_3 == 1)                                               //Touchsensor via de andere steen!!
                {
                            ExitTo(STEEN_ONTWIJKEN);
                }
    }
}
 
task STEEN_ONTWIJKEN()
{
     OnRev(motoren,100);
     Wait(500);
     if(SENSOR_3 <= 30)
     {
                 ExitTo(anderekant);
     }
     else
     {
         OnRev(OUT_C,40);
         OnFwd(OUT_A,40);
         Wait(kwartdraai1);
         Off(motoren);
         OnRev(motoren,100);
         if(SENSOR_4 >= 20)
         {
                     OnRev(OUT_C,40);
                     OnRev(OUT_A,80);
                     Wait(kwartdraai3);
                     OnRev(motoren,100);
         }
         if(SENSOR_4 >= 20)
         {
                     OnRev(OUT_C,40);
                     OnRev(OUT_A,80);
                     Wait(kwartdraai3);
                     OnRev(motoren,100);
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
}

task anderekant()
{
     OnRev(OUT_A,40);
     OnFwd(OUT_C,40);
     Wait(kwartdraai1);
     Off(motoren);
     OnRev(motoren,100);
     if(SENSOR_3 <= 20)
     {
                 OnRev(OUT_A,40);
                 OnRev(OUT_C,80);
                 Wait(kwartdraai3);
                 OnRev(motoren,100);
     }
     if(SENSOR_2 <= zwart2)
     {
                 Off(OUT_C);
                 OnRev(OUT_A,100);
                 if(SENSOR_1 <= zwart1)
                 {
                             OnFwd(OUT_A,100);
                             OnRev(OUT_C,100);
                             ExitTo(lijnvolger);
                 }
     }
}

task lijnvolger()
{
     OnRev(motoren,100);
}
