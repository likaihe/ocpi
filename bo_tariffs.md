# _Tariffs_ module

**Module Identifier: tariffs**

*General description of the business object*



## 1. Inheritances

*List all inheritors.*

### 1.1 Inheritor #1

*Describe the purpose and singularity of this inheritor.*



## 2. Flow and Lifecycle

*Describe the status of the objects, how it is created and destroyed,
when and through which action it gets inherited. Name the owner. Explain
the purpose.*




## 3. Interfaces and endpoints

*Explain which interfaces are available and which party should implement
which one.*


### 3.1 CPO Interface

The CPO Tariffs interface give the eMSP the ability to request all tariffs.

Example endpoint structure: `/ocpi/cpo/2.0/tariffs/`

| Method   | Description                                          |
| -------- | ---------------------------------------------------- |
| GET      | Returns all Tariff Objects from the CPO              |
| POST     | n/a                                                  |
| PUT      | n/a                                                  |
| PATCH    | n/a                                                  |
| DELETE   | n/a                                                  |


### 3.2 eMSP Interface

The Tariff information can also be pushed to the eMSP, for this the following needs to be implemented.

Example endpoint structure: `/ocpi/emsp/2.0/tariffs/`

| Method   | Description                                          |
| -------- | ---------------------------------------------------- |
| GET      | n/a                                                  |
| POST     | n/a                                                  |
| PUT      | Push all the Tariff Objects to the eMSP, same as GET on the CPO interface, but then instantiated by the other end-point. |
| PATCH    | Update a Tariff Object with new information          |
| DELETE   | Remove a Tariff Object which is no longer used/valid |



## 4. Object description

*Describe the structure of this object.*

### 4.1 Tariff

| Property        | Type          | Card. | Description                                                                           |
|-----------------|---------------|-------|---------------------------------------------------------------------------------------|
| id              | string(15)    | 1     | Uniquely identifies the tariff within the CPOs platform (and suboperator platforms).  |
| currency        | string(3)     | 1     | Currency of this tariff, ISO 4217 Code                                                |
| elements        | TariffElement | 1     | List of tariff elements                                                               |


## 5. Data types

*Describe all datatypes used in this object*

### 5.1 DayOfWeek

| Value        | Description                                          |
| ------------ | ---------------------------------------------------- |
| MONDAY       | Monday                                               |
| TUESDAY      | Tuesday                                              |
| WEDNESDAY    | Wednesday                                            |
| THURSDAY     | Thursday                                             |
| FRIDAY       | Friday                                               |
| SATURDAY     | Saturday                                             |
| SUNDAY       | Sunday                                               |


### 5.2 PriceComponent

| Property        | Type          | Card. | Description                                      |
|-----------------|---------------|-------|--------------------------------------------------|
| type            | DimensionType | 1     | Type of tariff dimension, see: [Types](types.md) |
| price           | decimal       | 1     | price per unit for this tariff dimension         |
| step_size       | int           | 1     | Minimum amount to be billed. This unit will be billed in this step_size blocks. For example: if type is time and  step_size is 300, then time will be billed in blocks of 5 minutes, so if 6 minutes is used, 10 minutes (2 blocks of step_size) will be billed. |


### 5.3 TariffElement

| Property         | Type               | Card. | Description                                                      |
|------------------|--------------------|-------|------------------------------------------------------------------|
| price_components | PriceComponent     | +     | List of price components that make up the pricing of this tariff |
| restrictions     | TariffRestrictions | ?     | List of tariff restrictions                                      |


### 5.4 TariffRestrictions

| Property        | Type               | Card. | Description                                                                           |
|-----------------|--------------------|-------|---------------------------------------------------------------------------------------|
| start_time      | string(5)          | ?     | Start time of day, for example 13:30, valid from this time of the day                 |
| end_time        | string(5)          | ?     | End time of day, for example 19:45, valid until this time of the day                  |
| start_date      | string(10)         | ?     | Start date, for example: 2015-12-24, valid from this day                              |
| end_date        | string(10)         | ?     | End date, for example: 2015-12-27, valid until this day (excluding this day)          |
| min_kwh         | decimal            | ?     | Minimum used energy in kWh, for example 20, valid from this amount of energy is used  |                             
| max_kwh         | decimal            | ?     | Maximum used energy in kWh, for example 50, valid until this amount of energy is used |
| min_power       | decimal            | ?     | Minimum power in kW, for example 0, valid from this charging speed                    |
| max_power       | decimal            | ?     | Maximum power in kW, for example 20, valid up to this charging speed                  |
| min_duration    | int                | ?     | Minimum duration in seconds, valid for a duration from x seconds                      |
| max_duration    | int                | ?     | Maximum duration in seconds, valid for a duration up to x seconds                     |
| day_of_week     | DayOfWeek          | *     | Which day(s) of the week this tariff is valid                                         |


