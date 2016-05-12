---
title: Ferries Data Structure
keywords: transportation, ferries data structure
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/ferries
---

The structure of the API specification follows a standard. This document
intends to explain every aspect of this structure and their fields.

|

The integration will have the following methods:

|

  -------------------------------------------------------------------------
  Method         Input          Output         Requir Description
                                               ed     
  -------------- -------------- -------------- ------ ---------------------
  Avail          AvailabilityRQ AvailabilityRS Yes    Makes a availability
                                                      call

  Valuation      ValuationRQ    ValuationRS    Yes    Makes a pre-booking

  Reservation    ReservationRQ  ReservationRS  Yes    Makes a booking

  Routes         RoutesRQ       RoutesRS       Yes    Gets a static routes
                                                      list

  RetrieveReserv RetrieveReserv RetrieveReserv No     Gets the details of a
  ation          ationRQ        ationRS               single booking

  RetrieveReserv RetrieveReserv RetrieveReserv No     Gets a list of
  ationList      ationListRQ    ationListRS           bookings

  Cancelation    CancellationRQ CancellationRS No     Cancels a booking
  -------------------------------------------------------------------------

|

Each request sent to the **service url** requires a node called rqXML .
Inside this node travels the current method's Input object.

|

The data structure will always have common elements in all objects and
the specific objects related to the operation

|

**Data structure content:**

> maxdepth
>
> :   3
>
> numbered
>
> :   
>
> Common-Elements\<./DSF/common/common-elements-ferries.rst\>
> Avail\<./DSF/ferries/avail.rst\>
> Valuation\<./DSF/ferries/valuation.rst\>
> Reservation\<./DSF/ferries/reservation.rst\> Routes
> \<./DSF/ferries/routes.rst\> Retrieve Reservation
> \<./DSF/ferries/retrieveReservation.rst\> Retrieve Reservation List
> \<./DSF/ferries/retrieveReservationList.rst\> Cancellation
> \<./DSF/ferries/cancel.rst\>