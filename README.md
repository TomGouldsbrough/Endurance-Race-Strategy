# Endurance-Race-Strategy
This Program takes the csv file from iracing to then calculate the fastest strategy by comparing the data from iracing against the amount of distance travelled.
The program is coded in matlab due to the ease of inputting csv files.
The code is shown below as a backup to the file.
FastestLap = 10000000;
FastestLapCount = 3;
FLCountNum = 0;
LengthOfRaceMins = input('enter the length of the race in minutes');
FuelLitres = input('enter the Fuel load of the car');

LapCount = input('enter the amount of laps you completed');
Laps2 = LapCount + 3;

while FastestLapCount ~= Laps2  
   FlVar = DataLoggedCSV.LapCurrentLapTimes1(FastestLapCount);
   if FlVar > 50
        if FastestLap > FlVar
            FastestLap = FlVar;
            FLCountNum = FastestLapCount;
        end
        

       
   end

FastestLapCount = FastestLapCount + 1;
end
LapDistanceE = (DataLoggedCSV.LapDistancem(FLCountNum))/1000;
LapDistance = sprintf('%10.2f',LapDistanceE);
disp(LapDistance)

StintLengthCount = 3;
StintLength = 0;

while StintLengthCount ~= Laps2
    stintlengthVar = DataLoggedCSV.LapCurrentLapTimes1(StintLengthCount);
    StintLength = StintLength + stintlengthVar;
    StintLengthCount = StintLengthCount + 1;
    


end

StintLengthMinsE = StintLength / 60;
StintLengthMins = sprintf('%10.2f',StintLengthMinsE);
StintLengthMinsWithPit = StintLengthMins + 1.12;

NumberOfStints = LengthOfRaceMins / StintLengthMinsE;

StrategyWorkBook1.NumberOfStints(1) = NumberOfStints;

FuelPerLap = -(DataLoggedCSV.FuelLevell2(FLCountNum));
StrategyWorkBook1.FuelPerLap(1) = FuelPerLap;


%Enters the distance of the lap in km, 2dp
StrategyWorkBook1.StrategyLapLength(1) = LapDistanceE;



%Enters the fastest lap instead of an average lap as this would include pit
%stop time which is entered after

StrategyWorkBook1.LapTime(1) = FastestLap;


%Amount of Fuel in the Car, inputted.

StrategyWorkBook1.Fuel(1) = FuelLitres;


%StintLength in minutes

StrategyWorkBook1.StintLengthMins(1) = StintLengthMinsE;


%LengthOfRace in Minutes#

StrategyWorkBook1.lengthMins(1) = LengthOfRaceMins;


%Number of stints not needing to fuel save
StintsInt = floor(NumberOfStints);

NumberOfStintsWOFuelSaving = (NumberOfStints - StintsInt) * LapCount;

StrategyWorkBook1.StintsWithoutFuelSaving(1) = NumberOfStintsWOFuelSaving;
%Pit Time_ inputted for now

PitTime = input('enter the pit time');

StrategyWorkBook1.PitTime(1) = PitTime;

%StintLengthWithPit
StintLengthMinsWPit = StintLengthMinsE + PitTime;

StrategyWorkBook1.StintLengthMinsWithPit(1) = StintLengthMinsWPit;


%StintLength
StintLength = LapDistanceE * LapCount;
StrategyWorkBook1.TotalDistancePerStint(1) = StintLength;

%TotalDistance

TotalDistance = StintLength * NumberOfStints;

StrategyWorkBook1.TotalDistance(1) = TotalDistance;

%TotalLaps

TotalLaps = TotalDistance / LapDistanceE;

StrategyWorkBook1.TotalLaps(1) = TotalLaps;





