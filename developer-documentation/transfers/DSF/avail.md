---
title: Availability
keywords: transfers, availability, avail
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/DSF/avail
---

|

Method Goals
============

This method aims to return all the available options for a given dates
and destinations.

|

Remarks
=======

This method **must** be called **before** the RateRule method.

|

AvailabilityRQ Example
======================

:

    <AvailabilityRQ>
        <echoToken>test</echoToken>
        <timeoutMilliseconds>60000</timeoutMilliseconds>
        <source>
            <agencyCode>xxxx</agencyCode>
            <languageCode>xx</languageCode>
        </source>
        <filterAuditData>
            <registerTransactions>true</registerTransactions>
        </filterAuditData>
        <Configuration codeProvider = "xxx">
            <Credentials user = "xxxx" password = "xxxx">
                <UrlGeneric>xxxx</UrlGeneric>
                <UrlIdentification xsi:nil = "true"/>
                <UrlAvailability xsi:nil = "true"/>
                <UrlRateRule xsi:nil = "true"/>
                <UrlBook xsi:nil = "true"/>
                <UrlsSpecific xsi:nil = "true"/>
            </Credentials>
            <Attributes>
            </Attributes>
        </Configuration>
        <Segments>
            <Segment id = "0">
                <Origin type = "ARP" code = "xxx" date = "2014-09-19T17:15:00">
                    <FlightInfo flightNumber = "xxxx">
                        <Arrival terminal = "xxx" date = "2014-09-19T17:45:00"/>
                        <Departure terminal = "xxx" date = "2014-09-19T17:15:00"/>
                    </FlightInfo>
                </Origin>
                <Destination type = "HOT" code = "xxxx" date = "2014-09-30T00:00:00">
                    <HotelInfo name="xxxx" address="xxxxx"></HotelInfo>
                </Destination>
            </Segment>
            <Segment id = "1">
                <Origin type = "HOT" code = "xxxx" date = "2014-09-01T17:15:00"/>
                    <HotelInfo name="xxxx" address="xxxxx"></HotelInfo>
                </Origin>
                <Destination type = "ARP" code = "xxx" date = "2014-09-02T00:00:00">
                    <FlightInfo flightNumber = "xxxx">
                        <Arrival terminal = "xxx" date = "2014-09-01T16:25:00"/>
                        <Departure terminal = "xxx" date = "2014-09-01T15:55:00"/>
                    </FlightInfo>
                </Destination>
            </Segment>
        </Segments>
        <Passengers>
            <Passenger id = "0" age = "30">
                <RefSegments>
                    <RefSegment refSegment = "0" bags = "0"/>
                    <RefSegment refSegment = "1" bags = "0"/>
                </RefSegments>
            </Passenger>
        </Passengers>
    </AvailabilityRQ>

|

AvailabilityRQ Description
==========================

The availability request is very straight forward. It only requires a
list of segments and a list of passengers. Each segment represents the
route that a transfer has to do, it contains the origin and destination
codes and dates. If the segment contains an Hotel destination or an
Airport destination, extra information must be sent in FlightInfo object
and HotelInfo object.

  -------------------------------------------------------------------------
  Element   Nu Type   Description
            mb        
            er        
  --------- -- ------ -----------------------------------------------------
  Availabil 1         Root Node
  ityRQ               

  Availabil 1  Config Configuration needed to send the transaction to the
  ityRQ/Con    uratio provider.
  figuratio    nProvi 
  n            der    

  Availabil 1  Segmen Contains a List of Segment. Each segment represents
  ityRQ/Seg    ts     the route that a transfer has to do, it contains the
  ments               origin and destination codes and dates.

  Availabil 1. Segmen Each segment represents the route that a transfer has
  ityRQ/Seg .n t      to do
  ments/Seg           
  ment                

  @Segment/ 1  Intege Integer that contains the ID of the Segment.
  id           r      

  @Segment/ 1  Locati This location object contains information related to
  Origin       on     the origin of the transfer.

  @Segment/ 1  Locati This location object contains information related to
  Destinati    on     the destination of the transfer.
  on                  

  @Location 1  eLocat Indicates the location type. The possible values are:
  /type        ionTyp **CTY**(City); **ZON**(Zone); **ARP**(Airport)
               e      **STA**(Train/Bus station); **PRT**(Port);
                      **HOT**(Hotel); **PDI**(Point of interest);
                      **OTH**(Other)

  @Location 1  String Code that identifies the location in the provider's
  /code               system.

  @Location 1  DateTi Indicates the date associated with this location.
  /date        me     

  @Location 0. Flight Contains a flight information if this location is an
  /FlightIn .1 Info   airport.
  fo                  

  @Location 1  String Indicates the flight number.
  /FlightIn           
  fo/flight           
  Number              

  @Location 1  Termin Contains the information related to the departure
  /FlightIn    alInfo terminal
  fo/Depart           
  ure                 

  @Location 1  Termin Contains the information related to the arrival
  /FlightIn    alInfo terminal.
  fo/Arriva           
  l                   

  @Terminal 1  String Indicates the code that identifies the terminal on
  Info/term           the providers system.
  inal                

  @Terminal 1  DateTi Indicates the date in which the customer must arrive
  Info/date    me     or depart.

  @Location 0. HotelI Contains an hotel information if this location is an
  /HotelInf .1 nfo    hotel.
  o                   

  @HotelInf 1  String Indicates the full name of the hotel (as it appears
  o/name              in the provider's system).

  @HotelInf 1  String Indicates the address of the hotel.
  o/address           

  Availabil 1  Passen Contains the passengers that are involved in the
  ityRQ/Pas    gers   reservation.
  sengers             

  Availabil 1. Passen Contains the passenger information.
  ityRQ/Pas .n ger    
  sengers/P           
  assenger            

  @Passenge 1  Intege This id identifies the passenger.
  r/id         r      

  @Passenge 1  Intege Indicates the age of the passenger.
  r/age        r      

  @Passenge 1  RefSeg Contains a list of references to the segments where
  r/RefSegm    ments  the passenger wants to be transfered.
  ents                

  @Passenge 1. RefSeg Contains a list of references to segments.
  r/RefSegm .n ment   
  ents/RefS           
  egment              

  @RefSegme 1  Intege This reference represents the id of the segment which
  nt/refSeg    r      is served with this option.
  ment                

  @RefSegme 1  Intege Indicates the number of bags carried by the
  nt/bags      r      passenger.
  -------------------------------------------------------------------------

|

AvailabilityRS Example
======================

:

    <AvailabilityRS>
        <auditData>
            <transactions>
                <timeStamp>2014-09-19T13:42:56.304353+01:00</timeStamp>
                <RQ>xxxx</RQ>
                <RS>xxxx</RS>
            </transactions>
            <timeStamp>2014-09-19T13:42:54.5681506+01:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <Transfers>
            <Transfer id = "0">
                <Info type = "BUS" code = "XXX" typeVeh = "XXX"/>
                <LocOrigin type = "ARP" code = "PMI" date = "2014-09-19T17:17:00"/>
                <LocDestination type = "HOT" code = "XXX" date = "0001-01-01T00:00:00"/>
            </Transfer>
            <Transfer id = "1">
                <Info type = "PRV" code = "XXX" typeVeh = "XXXX"/>
                <LocOrigin type = "ARP" code = "PMI" date = "2014-09-19T17:17:00"/>
                <LocDestination type = "HOT" code = "XXX" date = "0001-01-01T00:00:00"/>
            </Transfer>
            <Transfer id = "2">
                <Info type = "BUS" code = "XXX" typeVeh = "XXXX"/>
                <LocOrigin type = "ARP" code = "PMI" date = "2014-09-19T17:17:00"/>
                <LocDestination type = "HOT" code = "XXX" date = "0001-01-01T00:00:00"/>
            </Transfer>
            <Transfer id = "3">
                <Info type = "BUS" code = "XXX" typeVeh = "XXX"/>
                <LocOrigin type = "HOT" code = "XXX" date = "2014-09-01T17:17:00"/>
                <LocDestination type = "ARP" code = "PMI" date = "0001-01-01T00:00:00"/>
            </Transfer>
            <Transfer id = "4">
                <Info type = "PRV" code = "XXX" typeVeh = "XXX"/>
                <LocOrigin type = "HOT" code = "XXX" date = "2014-09-01T17:17:00"/>
                <LocDestination type = "ARP" code = "PMI" date = "0001-01-01T00:00:00"/>
            </Transfer>
            <Transfer id = "5">
                <Info type = "BUS" code = "XXX" typeVeh = "XXXX"/>
                <LocOrigin type = "HOT" code = "XXX" date = "2014-09-01T17:17:00"/>
                <LocDestination type = "ARP" code = "PMI" date = "0001-01-01T00:00:00"/>
            </Transfer>
        </Transfers>
        <Rates>
            <Rate id = "0" code = "0" providerCode = "XXX" rateType = "OW">
                <Options>
                    <Option status = "" id = "0" refSegment = "0">
                        <RefTransfers>
                            <RefTransfer refTransfer = "0" dateStart = "2014-09-19T17:17:00" dateEnd = "0001-01-01T00:00:00"/>
                        </RefTransfers>
                        <Parameters>
                        </Parameters>
                    </Option>
                </Options>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "BINDING"/>
                <RefTransfers>
                    <RefTransfer refTransfer = "0" dateStart = "2014-09-19T17:17:00" dateEnd = "0001-01-01T00:00:00"/>
                </RefTransfers>
            </Rate>
            <Rate id = "1" code = "1" providerCode = "XXX" rateType = "OW">
                <Options>
                    <Option status = "" id = "1" refSegment = "0">
                        <RefTransfers>
                            <RefTransfer refTransfer = "1" dateStart = "2014-09-19T17:17:00" dateEnd = "0001-01-01T00:00:00"/>
                        </RefTransfers>
                        <Parameters>
                        </Parameters>
                    </Option>
                </Options>
                <TotalRate currency = "EUR" amount = "39.060" priceType = "BINDING"/>
                <RefTransfers>
                    <RefTransfer refTransfer = "1" dateStart = "2014-09-19T17:17:00" dateEnd = "0001-01-01T00:00:00"/>
                </RefTransfers>
            </Rate>
           ...
        </Rates>
        <Errors>
            <Error>…</Error>
            <Error>…</Error>
            ...
        </Errors>
        <Warnings>
            <Warning>…</Warning>
            <Warning>…</Warning>
            ...
        </Warnings>
    </AvailabilityRS>

|

AvailabilityRS Description
==========================

The response of this method will contain a list of transfers and a list
of rates. The transfer object contains information related to the
vehicle that operates the transfer (it also contains the destination
codes and dates). Each received rate contains a pricing and a list of
options that reference a transfer on the transfer list. All the options
received in a rate have the same price. If the rate is OW their options
are combinable with options of other rates but if the rate is RT, they
are just combinable with other options of the same rate.

  -------------------------------------------------------------------------
  Elem N T Description
  ent  u y 
       m p 
       b e 
       e   
       r   
  ---- - - ----------------------------------------------------------------
  Avai 1   Root Node
  labi     
  lity     
  RS       

  Avai 1 T Contains a list of available transfers with its information.
  labi   r 
  lity   a 
  RS/T   n 
  rans   s 
  fers   f 
         e 
         r 
         s 

  Avai 1 T Contains a list of transfers.
  labi . r 
  lity . a 
  RS/T n n 
  rans   s 
  fers   f 
  /Tra   e 
  nsfe   r 
  r        

  @Tra 1 I This id identifies the transfer
  nsfe   n 
  r/id   t 
         e 
         g 
         e 
         r 

  @Tra 1 I Contains information related to the vehicle that operates the
  nsfe   n transfer.
  r/In   f 
  fo     o 
         T 
         r 
         a 
         n 
         s 
         f 
         e 
         r 

  @Inf 1 e This value classifies the vehicle in the following types:
  oTra   T **LIM**(Limousine); CAR(Car); **BUS**(Bus); **TAX**(Taxi);
  nsfe   r **PRV**(Private vehicle).
  r/ty   a 
  pe     n 
         s 
         f 
         e 
         r 
         T 
         y 
         p 
         e 

  @Inf 1 S Indicates the code of the transfer if the provider returns it.
  oTra   t 
  nsfe   r 
  r/co   i 
  de     n 
         g 

  @Inf 1 S Indicates the name of the transfer if the provider returns it.
  oTra   t 
  nsfe   r 
  r/na   i 
  me     n 
         g 

  @Inf 1 S Indicates the name of the transfer if the provider returns it.
  oTra   t 
  nsfe   r 
  r/ty   i 
  peVe   n 
  h      g 

  @Inf 1 S Indicates the code of the vehicle as it's returned in the
  oTra   t provider's response.
  nsfe   r 
  r/co   i 
  deVe   n 
  h      g 

  @Tra 1 L This location object contains information related to the origin
  nsfe   o of the transfer.
  r/Lo   c 
  cOri   a 
  gin    t 
         i 
         o 
         n 

  @Tra 1 L This location object contains information related to the
  nsfe   o destination of the transfer.
  r/Lo   c 
  cDes   a 
  tina   t 
  tion   i 
         o 
         n 

  @Tra 0 S This is a code that pairs an origin and a destination ( remark:
  nsfe . t contamplates the direction of the route ).
  r/ro . r 
  uteI 1 i 
  d      n 
         g 

  Avai 1 R Contains a list of available rates. From each rate there are
  labi   a available options and each option references the transfers that
  lity   t operate them.
  RS/R   e 
  ates   s 

  Avai 1 R Contains a list of Rate.
  labi . a 
  lity . t 
  RS/R n e 
  ates     
  /Rat     
  e        

  @Rat 1 I This id identifies the rate.
  e/id   n 
         t 
         e 
         g 
         e 
         r 

  @Rat 1 S Contains the code of the rate if the provider returns it.
  e/co   t 
  de     r 
         i 
         n 
         g 

  @Rat 1 S Contains the code of the provider that offers this rate.
  e/pr   t 
  ovid   r 
  erCo   i 
  de     n 
         g 

  @Rat 1 e Indicates if the rate is OW (one-way) or RT (return). The
  e/ra   R One-Way rates are combinable, but the return ones are not
  teTy   a combinable.
  pe     t 
         e 
         T 
         y 
         p 
         e 

  @Rat 1 O Contains a list of options that belong to this rate.
  e/Op   p 
  tion   t 
  s      i 
         o 
         n 
         s 

  @Opt 1 O Contains a list of OptionRate.
  ions . p 
  /Opt . t 
  ion  n i 
         o 
         n 
         R 
         a 
         t 
         e 

  @Opt 1 S Indicates the status of the option if the provider returns this
  ionR   t information. This is a plain text of the status returned by the
  ate/   r provider, this means that each provider may send it's own status
  stat   i codes/messages.
  us     n 
         g 

  @Opt 1 I This code identifies the option.
  ionR   n 
  ate/   t 
  id     e 
         g 
         e 
         r 

  @Opt 1 I This reference represents the id of the segment which is served
  ionR   n with this option.
  ate/   t 
  refS   e 
  egme   g 
  nt     e 
         r 

  @Opt 1 R Contains a list of references of different transfers that serve
  ionR   e the segment indicated on "refSegment" field
  ate/   f 
  RefT   T 
  rans   r 
  fers   a 
         n 
         s 
         f 
         e 
         r 
         s 

  @Opt 1 R 
  ionR . e 
  ate/ . f 
  RefT n T 
  rans   r 
  fers   a 
  /Ref   n 
  Tran   s 
  sfer   f 
         e 
         r 

  @Ref 1 I This reference represents the id of a transfer.
  Tran   n 
  sfer   t 
  /ref   e 
  Tran   g 
  sfer   e 
         r 

  @Ref 1 D Indicates the start date/time of the service.
  Tran   a 
  sfer   t 
  /dat   e 
  eSta   T 
  rt     i 
         m 
         e 

  @Ref 1 D Indicates the end date/time of the service.
  Tran   a 
  sfer   t 
  /dat   e 
  eEnd   T 
         i 
         m 
         e 

  @Opt 1 P Contains a list of Parameter objects. These objects contain
  ionR   a information that the integration needs to proceed with the
  ate/   r booking process. The information contained in this objects is
  Para   a not relevant for the agency but is really important to spread it
  mete   m during the booking process. This means that a parameter returned
  rs     e in AvailabilityRS should be received by the integration on
         t RateRuleRQ, returned on RateRuleRS and received by the
         e integration again on BookRQ. This is very important to ensure
         r the correct functionality of the integration. One of the most
         s typical Parameter's use is to spread a sessionID.

  @Opt 1 P This is a list of Parameter objects.
  ionR . a 
  ate/ . r 
  Para n a 
  mete   m 
  rs/P   e 
  aram   t 
  eter   e 
         r 

  @Par 1 S This is the key that identifies the parameter.
  amet   t 
  er/k   r 
  ey     i 
         n 
         g 

  @Par 1 S This is the value of the parameter.
  amet   t 
  er/v   r 
  alue   i 
         n 
         g 

  @Rat 1 P Contains information about the price of this rate.
  e/To   r 
  talR   i 
  ate    c 
         e 

  @Pri 1 S Indicates the currency in which the amount is represented.
  ce/c   t 
  urre   r 
  ncy    i 
         n 
         g 

  @Pri 1 D Indicates the total amount of the reservation. If the rate is OW
  ce/a   e this price correspond to each option included in this *Rate*
  moun   c object, if the rate is RT correspond to the pair of options
  t      i included in this *Rate* object.
         m 
         a 
         l 

  @Pri 1 e Contains the price type. The possible values are: **NET**: The
  ce/p   P returned price is a net price; **BINDING**: The returned price
  rice   r is a retail pric; **COMMISSION**: The returned price is
  Type   i commissionable.
         c 
         e 
         T 
         y 
         p 
         e 

  @Pri 1 D This value indicates the % of commission if the provider returns
  ce/c   e it.
  ommi   c 
  ssio   i 
  n      m 
         a 
         l 

  @Rat 1 R Contains a list of transfer references.
  e/Re   e 
  fTra   f 
  nsfe   T 
  rs     r 
         a 
         n 
         s 
         f 
         e 
         r 
         s 

  @Rat 1 R Contains a list of references of different transfers that serve
  e/Re . e the segment indicated on "refSegment" field
  fTra . f 
  nsfe n T 
  rs/R   r 
  efTr   a 
  ansf   n 
  er     s 
         f 
         e 
         r 
  -------------------------------------------------------------------------

|