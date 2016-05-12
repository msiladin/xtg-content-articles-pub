---
title: Booking
keywords: transfers, data structure, booking
sidebar: mydoc_sidebar
permalink: /developer-documentation/car/DSF/reservation
---

|

Method Goals
============

This method aims to book the selected vehicle.

|

Remarks
=======

|

OTA VehResRQ Example
====================

:

    <OTA_VehResRQ>
    <timeoutMilliseconds>60000</timeoutMilliseconds>
      <filterAuditData>
        <registerTransactions>false</registerTransactions>
      </filterAuditData>
      <Configuration ProviderCode="CT">
        <Credentials user="1234" password="">
          <genericURL>https://otatest.cartrawler.com:20000/cartrawlerota</genericURL>
          <identificationURL xsi:nil="true" />
          <availRateURL xsi:nil="true" />
          <rateRuleURL xsi:nil="true" />
          <vehResURL xsi:nil="true" />
          <specificURLs>
            <Attribute key="URL_OFICINAS" value="https://ota.cartrawler.com/cartrawlerota/files/static/ctlocation.EN.xml" />
          </specificURLs>
        </Credentials>
        <Attributes>
          <Attribute key="ISOCurrency" value="EUR" />
          <Attribute key="ConsumerIP" value="95.39.27.98" />
        </Attributes>
      </Configuration>
      <ClientConfiguration agency="agencyName" SellCurrency="EUR" />
        <POS>
            <Source ISOCountry = "ESP">
                <RequestorID Type = "LAN" ID = "es"/>
            </Source>
        </POS>
        <VehResRQCore Status = "Available">
            <VehRentalCore PickUpDateTime = "2012-11-29T09:30:00" ReturnDateTime = "2012-12-01T17:00:00">
                <PickUpLocation LocationCode = "PMI" CodeContext = "IATA"/>
                <ReturnLocation LocationCode = "PMI" CodeContext = "IATA"/>
            </VehRentalCore>
            <Customer>
                <Primary BirthDate = "17/07/1980 10:39:13">
                    <PersonName>
                        <GivenName>TEST_NOM</GivenName>
                        <Surname>TEST_COG</Surname>
                    </PersonName>
                    <Telephone PhoneTechType = "VOICE" PhoneNumber = "68181"/>
                    <Email>car@xmltravelgate.com</Email>
                    <Document DocID = "12345678M" DocType = "NATIONAL_IDENTITY_DOCUMENT"/>
                </Primary>
            </Customer>
            <VehPref AirConditionInd = "true" TransmissionType = "MANUAL">
                <VehType VehicleCategory = "1" doorCount = "2"/>
                <VehClass Size = "1"/>
                <VehMakeModel Name = "n/a" Code = "MBMR"/>
            </VehPref>
            <RateQualifier RateCategory = "3" RateQualifier = "GN"/>
            <TotalCharge RateTotalAmount = "106.00" CurrencyCode = "EUR"/>
            <UniqueID ID = "Travel123456" Type = "1"/>
        </VehResRQCore>
    </OTA_VehResRQ>

|

OTA VehResRQ Description
========================

The request format works the same way as the OTA VehRateRule request.
The main difference is that in addition to vehicle information, it is
also necessary the customer information.

  -------------------------------------------------------------------------
  Element  Nu Type         Description
           mb              
           er              
  -------- -- ------------ ------------------------------------------------
  OTA\_Veh 1               Root Node
  ResRQ                    

  OTA\_Veh 1  Pos          Contains information of the Point Of Sale.
  ResRQ/PO                 
  S                        

  OTA\_Veh 1  VehResRQCore Includes information about the customer and the
  ResRQ/Ve                 rental, such as dates, model, locations.
  hResRQCo                 
  re                       

  VehResRQ 1  eInventorySt Status of the option. It's possible values are
  Core/Sta    atus         Available, OnRequest and All.
  tus                      

  VehResRQ 1  VehRentalCor Contains the dates and locations of the rental.
  Core/Veh    e            
  RentalCo                 
  re                       

  VehResRQ 1  CustomerPrim Information of the customer.
  Core/Cus    aryAdditiona 
  tomer       l            

  VehResRQ 1  CompanyNameP Name of the rental company.
  Core/Ven    ref          
  dorPref                  

  VehResRQ 1  Identifies   
  Core/Ven    the company  
  dorPref/    that offers  
  Code        the option.  

  VehResRQ 1  VehiclePref  Information of the rented car.
  Core/Veh                 
  Pref                     

  VehResRQ 1  DriverType   Indicates the age of the driver.
  Core/Dri                 
  verType                  

  DriverTy 1  Integer      The age of the driver.
  pe/Age                   

  VehResRQ 1  RateQualifie Information about the selected rate.
  Core/Rat    r            
  eQualifi                 
  er                       

  VehResRQ 1  VehicleTotal Indicates the total cost of the rental.
  Core/Tot    ChargeGroup  
  alCharge                 

  VehResRQ 1  UniqueID     It has the UniqueID that identifies the
  Core/Uni                 reservation for the provider to cancel it.
  queID                    

  @UniqueI 1  String       ID of the locator that identifies the booking.
  D/ID                     

  @UniqueI 1  eUniqueIdTyp Type of locator. It's possible values are
  D/Type      e            CUSTOMER (if sent from a customer agency),
                           CORPORATIONREPRESENTATIVE (if sent by a third
                           party company), COMPANY (if sent by the provider
                           company).

  VehResRQ 1  TPAExtension Contains an Atributos object.
  Core/TPA    s            
  Extensio                 
  ns                       

  OTA\_Veh 1  VehResRQInfo Contains information about the credit card. It's
  ResRQ/Ve                 only mandatory when a credit card payment is
  hResRQIn                 needed.
  fo                       

  VehResRQ 1  ArrivalDetai Currently unused.
  Info/Arr    ls           
  ivalDeta                 
  ils                      

  VehResRQ 1  RentalPaymen Contains information needed if a card is
  Info/Ren    tPref        required.
  talPayme                 
  ntPref                   

  RentalPa 1  PaymentCard  Contains the information of the card for the
  ymentPre                 payment.
  f/Paymen                 
  tCard                    

  PaymentC 1  CardType     Indicates the type of card. It represents if the
  ard/Card                 card is Credit, Debit of a Central bill.
  Type                     

  PaymentC 1  String       Card code in the provider's format. Example:
  ard/Card                 "VI" for Visa.
  Code                     

  PaymentC 1  String       The number that identifies the card.
  ard/Card                 
  Number                   

  PaymentC 1  String       The month and year of expiration of the card in
  ard/Expi                 mmYY format.
  reDate                   

  PaymentC 1  The name     Indicates the owner of the reservation.
  ard/Card    that appears 
  HolderNa    on the card  
  me                       
  -------------------------------------------------------------------------

|

OTA VehResRS Example
====================

:

    <OTA_VehResRS>   
        <auditData>
            <transactions>
                <timeStamp>2013-06-12T13:30:51.6688071+02:00</timeStamp>
                <processTimeMilliseconds>0</processTimeMilliseconds>
            </transactions>
            <timeStamp>2013-06-12T13:30:47.5856234+02:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <VehResRSCore>
            <VehReservation ReservationStatus = "RESERVED">
                <VehSegmentCore>
                    <ConfID ID = "ES289589400" Type = "4"/>
                    <Vendor Code = "84"/>
                    <Vehicle AirConditionInd = "True" TransmissionType = "MANUAL" PassengerQuantity = "5" BaggageQuantity = "3" VendorCarType = "ECMR">
                        <VehType VehicleCategory = "1" doorCount = "2/4"/>
                        <VehClass Size = "3"/>
                        <VehMakeModel Name = "Peugeot 207 or similar" Code = "ECMR"/>
                        <PictureURL>https://cdn.cartrawler.com/otaimages/peugeot/207_nologo.jpeg</PictureURL>
                    </Vehicle>
                    <TotalCharge RateTotalAmount = "66.99" CurrencyCode = "EUR"/>
                </VehSegmentCore>
            </VehReservation>
        </VehResRSCore>
    </OTA_VehResRS>

|

OTA VehResRS Description
========================

The result returns a list of ConfID (booking codes). It can be the
supplier's or the one sent in the request. It also returns all the
charges associated to the booking.

  -------------------------------------------------------------------------
  Element      Nu Type    Description
               mb         
               er         
  ------------ -- ------- -------------------------------------------------
  OTA\_VehResR 1          Root Node
  S                       

  OTA\_VehResR 1  VehResR Contains the information of the reservation.
  S/vehResRSCo    SCore   
  re                      

  VehResRSCore 1  Vehicle Contains information about the reservation.
  /VehReservat    Reserva 
  ion             tion    

  VehicleReser 1  VehSegm Contains the confID that identifies the booking,
  vation/VehSe    entCore the selected vehicle and the total charge.
  gmentCore               

  VehicleSegme 1  List of Contains the confID that identifies the booking,
  ntCore/ConfI    ConfID  the selected vehicle and the total charge.
  D                       

  @ConfID/ID   1  String  ID of the locator that identifies the booking.

  @ConfID/Type 1  eUnique Type of locator. It's possible values are
                  Type    CUSTOMER (if sent from a customer agency),
                          CORPORATIONREPRESENTATIVE (if sent by a third
                          party company), COMPANY (if sent by the provider
                          company).

  VehicleSegme 1  Company Indicates the Company that rents the car.
  ntCore/Vendo    Name    
  r                       

  VehicleSegme 1  Vehicle Contains information about the vehicle.
  ntCore/Vehic            
  le                      

  VehicleSegme 1  Vehicle Indicates the total charge of the rental returned
  ntCore/Vehic    TotalCh by the provider.
  leTotalCharg    argeGro 
  eGroup          up      

  VehicleReser 1  eTransa Indicates the status of the reservation.
  vation/Reser    ctionSt 
  vationStatus    atusTyp 
                  e       
  -------------------------------------------------------------------------

|