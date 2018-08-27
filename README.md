#CJ_Ribbons_Crossover_Test_Study

input price = close;
input baseLength = 10;
input incrementOrMultiplier = 10;
input arithOrGeom1or2 = 1;
input trendLength = 2;
def na = Double.NaN;

plot XMA1;
plot XMA2;
plot XMA3;
plot XMA4;
plot XMA5;
plot XMA6;
plot XMA7;
plot XMA8;


if (arithOrGeom1or2 == 1)
then {
    XMA1 = ExpAverage(price, baseLength);
    XMA2 = ExpAverage(price, baseLength + 1 * incrementOrMultiplier);
    XMA3 = ExpAverage(price, baseLength + 2 * incrementOrMultiplier);
    XMA4 = ExpAverage(price, baseLength + 3 * incrementOrMultiplier);
    XMA5 = ExpAverage(price, baseLength + 4 * incrementOrMultiplier);
    XMA6 = ExpAverage(price, baseLength + 5 * incrementOrMultiplier);
    XMA7 = ExpAverage(price, baseLength + 6 * incrementOrMultiplier);
    XMA8 = ExpAverage(price, baseLength + 7 * incrementOrMultiplier);
} else {
    XMA1 = ExpAverage(price, baseLength);
    XMA2 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 1));
    XMA3 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 2));
    XMA4 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 3));
    XMA5 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 4));
    XMA6 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 5));
    XMA7 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 6));
    XMA8 = ExpAverage(price, baseLength * Power(incrementOrMultiplier, 7));
}

XMA1.SetDefaultColor(CreateColor(255, 65, 0));
XMA2.SetDefaultColor(CreateColor(255, 90, 0));
XMA3.SetDefaultColor(CreateColor(255, 115, 0));
XMA4.SetDefaultColor(CreateColor(255, 140, 0));
XMA5.SetDefaultColor(CreateColor(255, 165, 0));
XMA6.SetDefaultColor(CreateColor(255, 190, 0));
XMA7.SetDefaultColor(CreateColor(255, 215, 0));
XMA8.SetDefaultColor(CreateColor(255, 240, 0));

def crossover = if XMA1 > XMA8 then 1 else 0;
def crossunder = if XMA8 < XMA1 then 1 else 0;

#plot up = if crossover then low - TickSize() else na;
#plot down = if crossunder then high + TickSize() else na;
#up.SetPaintingStrategy(PaintingStrategy.ARROW_UP);
#down.SetPaintingStrategy(PaintingStrategy.ARROW_DOWN);

#Standard
#AddOrder(OrderType.BUY_AUTO, Sum(XMA1 < XMA8 and XMA2 < XMA8, trendLength)[1] == trendLength and XMA1 > XMA8, tickcolor = GetColor(1), arrowcolor = GetColor(1), name = "Crossover_Timing_Buy");


#CJ
AddOrder(OrderType.BUY_AUTO, Sum(XMA1 > XMA8 and XMA1 < XMA2, trendLength)[1] == trendLength and XMA1 > XMA2, tickcolor = GetColor(1), arrowcolor = GetColor(1), name = "Crossover_Timing_Buy");
AddOrder(OrderType.BUY_AUTO, Sum(XMA1 < XMA2 and XMA2 > XMA8, trendLength)[1] == trendLength and XMA1 > XMA2, tickcolor = GetColor(1), arrowcolor = GetColor(1), name = "Crossover_Timing_Buy");
AddOrder(OrderType.BUY_AUTO, Sum(XMA1 < XMA4 and XMA2 < XMA4, trendLength)[1] == trendLength and XMA1 > XMA4, tickcolor = GetColor(1), arrowcolor = GetColor(1), name = "Crossover_Timing_Buy");
AddOrder(OrderType.SELL_TO_CLOSE, Sum(XMA1 > XMA8 and XMA1 > XMA4, trendLength)[1] == trendLength and XMA1 < XMA4, tickcolor = GetColor(2), arrowcolor = GetColor(2), name = "Crossover_Timing_Sell");
AddOrder(OrderType.SELL_TO_CLOSE, Sum(XMA1 > XMA8, trendLength)[1] == trendLength and XMA1 < XMA8, tickcolor = GetColor(2), arrowcolor = GetColor(2), name = "Crossover_Timing_Sell");




# README #

This README would normally document whatever steps are necessary to get your application up and running.

### What is this repository for? ###

* Quick summary
* Version
* [Learn Markdown](https://bitbucket.org/tutorials/markdowndemo)

### How do I get set up? ###

* Summary of set up
* Configuration
* Dependencies
* Database configuration
* How to run tests
* Deployment instructions

### Contribution guidelines ###

* Writing tests
* Code review
* Other guidelines

### Who do I talk to? ###

* Repo owner or admin
* Other community or team contact