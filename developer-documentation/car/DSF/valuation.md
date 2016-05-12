---
title: OTA VehRetRes (Get Booking Details)
keywords: transfers, data structure, valuation
sidebar: mydoc_sidebar
permalink: /developer-documentation/car/DSF/valuation
---

|

Method Goals
============

This method aims to retrieve a booking with its full details.

|

Remarks
=======

Some suppliers do not implement this method.

|

OTA VehRetResRQ Example
=======================

:

    <OTA_VehRetResRQ>
        <POS>
            <Source ISOCountry = "ESP">
                <RequestorID Type = "LAN" ID = "es"/>
            </Source>
        </POS>
        <VehRetResRQCore>
            <UniqueID ID = "4564894564" Type = "4"/>
            <PersonName>
                <GivenName>TEST</GivenName>
                <Surname>TEST</Surname>
            </PersonName>
        </VehRetResRQCore>
    </OTA_VehRetResRQ>

|

OTA\_VehRetResRQ Description
============================

The request requires the UniqueID (locator) of the reservation and the
name of the customer to identify the reservation and retrieve its
information.

  ------------------------------------------------------------------------
  Element        Numb Type    Description
                 er           
  -------------- ---- ------- --------------------------------------------
  OTA\_VehRetRes 1            Root Node
  RQ                          

  OTA\_VehRetRes 1    Pos     Contains information of the Point Of Sale.
  RQ/POS                      

  OTA\_VehRetRes 1    VehRetR Contains the locator and the name of the
  RQ/VehRetResRQ      esRQCor customer in order to identify and retrieve
  Core                e       the booking information.

  VehRetResRQCor 1    UniqueI It has the UniqueID that identifies the
  e/UniqueID          D       reservation for the provider to cancel it.

  VehRetResRQCor 1    PersonN Contains the name of the customer that made
  e/PersonName        ame     the reservation.
  ------------------------------------------------------------------------

|

OTA\_VehRetResRS Example
========================

:

    <OTA_VehRetResRS>
        <Success/>
        <VehRetResRSCore>
            <VehReservation ReservationStatus = "">
                <VehSegmentCore>
                    <ConfID ID = " " Type = ""/>
                    ...
                    <Vendor Code = " "/>
                    <Vehicle AirConditionInd = " " TransmissionType = " " VendorCarType = " ">
                        <VehMakeModel Name = "" Code = ""/>
                        <VehType DoorCount = "" VehicleCategory = ""/>
                        <VehClass Size = ""/>
                    </Vehicle>
                    <TotalCharge CurrencyCode = " " RateTotalAmount = ""/>
                </VehSegmentCore>
            </VehReservation>
        </VehRetResRSCore>
        <Errors>
            <Error></Error>
            ...
        </Errors>
        <Warnings>
            <Warning>…</Warning>
            ...
        </Warnings>
    </OTA_VehRetResRS>

|

OTA VehRetResRS Description
===========================

The result returns the full details of a booking. It is very similar to
the OTA VehRes Response.

  -------------------------------------------------------------------------
  Element                Numbe Type            Description
                         r                     
  ---------------------- ----- --------------- ----------------------------
  OTA\_VehRetResRS       1                     Root Node

  OTA\_VehRetResRS/VehRe 1     VehicleRetrieve Contains the information of
  tResRSCore                   ResRSCore       the retrieved booking.

  VehicleRetrieveResRSCo 1     VehicleReservat Contains the information of
  re/VehReservation            ion             the retrieved booking.
  -------------------------------------------------------------------------

|