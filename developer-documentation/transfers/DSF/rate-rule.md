---
title: RateRule (Pre-Booking)
keywords: transfers, rate rule
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/DSF/rate-rule
---

|

Method Goals
============

This method aims to return price of the SelectedOptions . This options
**must** be selected in the previous step ( Availability ).

This message allows the partners to know the applied conditions on the
chosen transfers.

|

Remarks
=======

Some suppliers do not provide this method. If this is the case, our
integration will internally call an Availability method and will filter
the results in order to refresh the information and produce a RateRuleRS
.

|

RateRule RQ Example
===================

:

    <RateRuleRQ>
       <timeoutMilliseconds>60000</timeoutMilliseconds>
        <source>
            <agencyCode>test</agencyCode>
            <languageCode>es</languageCode>
        </source>
        <filterAuditData>
            <registerTransactions>true</registerTransactions>
        </filterAuditData>
        <Configuration codeProvider = "XXX">
            <Credentials user = "XXXX" password = "XXXX">
                <UrlGeneric>XXX</UrlGeneric>
                <UrlIdentification xsi:nil = "true"/>
                <UrlAvailability xsi:nil = "true"/>
                <UrlRateRule xsi:nil = "true"/>
                <UrlBook xsi:nil = "true"/>
                <UrlsSpecific xsi:nil = "true"/>
            </Credentials>
            <Attributes>
            </Attributes>
        </Configuration>
        <SelectedRates>
            <SelectedRate id = "0" code = "0" providerCode = "XXX" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "" id = "0">
                        <Segment id = "0">
                            <Origin type = "ARP" code = "XXX" date = "2014-09-19T17:15:00">
                                <FlightInfo flightNumber = "XXX">
                                    <Arrival terminal = "XXX" date = "2014-09-19T17:45:00"/>
                                    <Departure terminal = "XXX" date = "2014-09-19T17:15:00"/>
                                </FlightInfo>
                            </Origin>
                            <Destination type = "HOT" code = "XXX" date = "2014-09-30T00:00:00"/>
                        </Segment>
                        <Transfers>
                            <Transfer id = "0">
                                <Info type = "BUS" code = "XXXX" typeVeh = "XXX"/>
                                <LocOrigin type = "ARP" code = "XXX" date = "2014-09-19T17:17:00"/>
                                <LocDestination type = "HOT" code = "XXX" date = "0001-01-01T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters>
                        </Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "BINDING"/>
                <CancellationPolicy/>
            </SelectedRate>
            <SelectedRate id = "5" code = "5" providerCode = "XXX" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "" id = "5">
                        <Segment id = "0">
                            <Origin type = "ARP" code = "XXX" date = "2014-09-19T17:15:00">
                                <FlightInfo flightNumber = "XXX">
                                    <Arrival terminal = "XXX" date = "2014-09-19T17:45:00"/>
                                    <Departure terminal = "XXX" date = "2014-09-19T17:15:00"/>
                                </FlightInfo>
                            </Origin>
                            <Destination type = "HOT" code = "XXX" date = "2014-09-30T00:00:00"/>
                        </Segment>
                        <Transfers>
                            <Transfer id = "5">
                                <Info type = "BUS" code = "XXX" typeVeh = "XXX"/>
                                <LocOrigin type = "HOT" code = "XXX" date = "2014-09-01T17:17:00"/>
                                <LocDestination type = "ARP" code = "XXX" date = "0001-01-01T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters>
                        </Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "23.390" priceType = "BINDING"/>
                <CancellationPolicy/>
            </SelectedRate>
        </SelectedRates>
        <Passengers>
            <Passenger id = "0" age = "30">
                <RefSegments>
                    <RefSegment refSegment = "0" bags = "0"/>
                    <RefSegment refSegment = "1" bags = "0"/>
                </RefSegments>
            </Passenger>
        </Passengers>
    </RateRuleRQ>

|

RateRule RQ Description
=======================

The RateRule request requires the following information:

-   The selected rates with their corresponding selected options.
-   The passengers of the booking.

  --------------------------------------------------------------------------
  Element    Nu Type  Description
             mb       
             er       
  ---------- -- ----- ------------------------------------------------------
  RateRuleRQ 1        Root Node

  RateRuleRQ 1  Selec Contains a list with the selected rates from
  /SelectedR    tedRa availability response.
  ates          tes   

  RateRuleRQ 1. Selec Contains a list of SelectedRate.
  /SelectedR .n tedRa 
  ates/Selec    te    
  tedRate             

  @SelectedR 1  Integ This id identifies the rate.
  ate/id        er    

  @SelectedR 1  Strin Contains the code of the rate if the provider returns
  ate/code      g     it.

  @SelectedR 1  Strin Contains the code of the provider that offers this
  ate/provid    g     rate.
  erCode              

  @SelectedR 1  eRate Indicates if the rate is OW (one-way) or RT (return).
  ate/rateTy    Type  
  pe                  

  @SelectedR 1  Selec Contains a list of SelectedOptions that belong to this
  ate/Select    tedOp rate.
  edOptions     tions 

  @SelectedR 1. Selec Contains a list of SelectedOption.
  ate/Select .n tedOp 
  edOptions/    tion  
  SelectedOp          
  tion                

  @SelectedO 1  Strin Indicates the status of the option if the provider
  ption/stat    g     returns this information. This is a plain text of the
  us                  status returned by the provider, this means that each
                      provider may send it's own status codes/messages.

  @SelectedO 1  Integ This code identifies the option.
  ption/id      er    

  @SelectedO 1  Segme Contains the segment which is served with this option.
  ption/Segm    nt    
  ent                 

  @SelectedO 1  Trans Contains a list of different transfers that serve the
  ption/Tran    fers  segment of this option.
  sfers               

  @SelectedO 1. Trans Contains a list of transfers which is served with this
  ption/Tran .n fer   option.
  sfers/Tran          
  sfer                

  @SelectedO 1  Param Contains a list of Parameter objects. The parameter
  ption/Para    eters returned in AvailabilityRS should be received by the
  meters              integration on RateRuleRQ.

  @SelectedR 1  Price Contains information about the price of this rate. If
  ate/TotalR          the rate is OW this price correspond to each option
  ate                 included in this *SelectedRate* object, if the rate is
                      RT correspond to the pair of options included in this
                      *SelectedRate* object.

  @SelectedR 1  Cance Contains a list of conditions of the penalties for the
  ate/Cancel    llati cancellation of the reservation. This object normaly
  lationPoli    onPol is not used because in this moments the providers not
  cy            icies return this informacion in *AvailabilityRS*, if there
                      are any will be returned in *RateRuleRS*.

  RateRuleRQ 1  Passe Contains a list of the passengers that participate in
  /Passenger    ngers this reservation.
  s                   

  RateRuleRQ 1. Passe Contains a list of Passenger objects.
  /Passenger .n nger  
  s/Passenge          
  r                   
  --------------------------------------------------------------------------

|

RateRuleRS Example
==================

:

    <RateRuleRS>
        <auditData>
            <transactions>
                <timeStamp>2014-09-19T13:43:32.2921652+01:00</timeStamp>
                <RQ></RQ>
                <RS></RS>
            </transactions>
            <transactions>
                <timeStamp>2014-09-19T13:43:33.79646+01:00</timeStamp>
                <RQ></RQ>
                <RS></RS>
            </transactions>
            <timeStamp>2014-09-19T13:43:30.7950125+01:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <SelectedRates>
            <SelectedRate id = "0" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "NEW" id = "0">
                        <Transfers>
                            <Transfer id = "0">
                                <Info type = "BUS" code = "XXX" typeVeh = "XXX">
                                    <vendorMessages>
                                        <vendorMessage>
                                            <Tittle>XXX</Tittle>
                                            XXXXXXXXXXXXXXXXXXXXXX
                                        </vendorMessage>
                                    </vendorMessages>
                                </Info>
                                <LocOrigin type = "ARP" code = "PMI" date = "2014-09-19T00:00:00"/>
                                <LocDestination type = "HOT" code = "XXX" date = "2014-09-19T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters></Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "NET" commission = "0.640"/>
            </SelectedRate>
            <SelectedRate id = "0" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "NEW" id = "0">
                        <Transfers>
                            <Transfer id = "0">
                                <Info type = "BUS" code = "XXX" typeVeh = "XXX">
                                    <vendorMessages>
                                        <vendorMessage>
                                            <Tittle>XXXX</Tittle>
                                            XXXXXXXXXX
                                        </vendorMessage>
                                    </vendorMessages>
                                </Info>
                                <LocOrigin type = "ARP" code = "XXX" date = "2014-09-19T00:00:00"/>
                                <LocDestination type = "HOT" code = "XXX" date = "2014-09-19T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters></Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "NET" commission = "0.640"/>
            </SelectedRate>
        </SelectedRates>
        <Warnings> 
            <Warning>…</Warning>
                . . .
        </Warnings> 
        <Errors>
            <Error>…</Error>
            . . .    
        </Errors>
     </RateRuleRS>

|

RateRuleRS Description
======================

The returned XML is similar to the result of the Availability call. The
main difference is that instead of receiving Rates the client receives a
list of SelectedRate . This object is almost the same as a Rate but it
contains the transfer information instead of just a reference and it
contains messages with important information from the provider.

  -------------------------------------------------------------------------
  Element              Num Type  Description
                       ber       
  -------------------- --- ----- ------------------------------------------
  RateRuleRS           1         Root Node

  RateRuleRS/SelectedR 1   Selec Contains a list of the requested selected
  ates                     tedRa rates. The information of this rates is
                           tes   refreshed with the new information
                                 received from the provider.

  RateRuleRS/SelectedR 1.. Selec Contains a list of SelectedRate.
  ates/SelectedRate    n   tedRa 
                           te    

  @SelectedRate/Select 1   InfoT Contains information related to the
  edOptions/SelectedOp     ransf vehicle that operates the transfer.
  tion/Transfers/Trans     er    
  fer/Info                       

  @InfoTransfer/vendor 1.. vendo Contains vendorMessage objects that have
  Messages             n   rMess important information about the transfer.
                           age   

  @vendorMessage/Langu 1   Strin Indicates the language in which the text
  age                      g     is written.

  @vendorMessage/Tittl 1   Strin Tittle of the message
  e                        g     

  @vendorMessage/Text  1   Strin Contains the text.
                           g     
  -------------------------------------------------------------------------

|