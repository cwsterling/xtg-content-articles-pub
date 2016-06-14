﻿---
title: Hotel XSD
keywords: common elements, elements, hotel
sidebar: mydoc_sidebar
permalink: /docs/hotel/hotel
---

~~~xml
<?xml version="1.0"?>
<xs:schema elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="AvailRQ" nillable="true" type="AvailRQ" />
  <xs:complexType name="AvailRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="1" maxOccurs="1" name="SearchType" type="eTypeSearch" />
          <xs:element minOccurs="1" maxOccurs="1" name="CancellationPolicies" type="xs:boolean" />
		  <xs:element minOccurs="1" maxOccurs="1" name="OnRequest" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="BusinessRules" type="eTypeBusinessRule" />
          <xs:element minOccurs="0" maxOccurs="1" name="AvailDestinations" type="AvailDestinations" />
          <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Currency" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Nationality" type="xs:string" />		  
          <xs:element minOccurs="0" maxOccurs="1" name="RoomCandidates" type="RoomCandidates" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="HotelBaseRQ" abstract="true">
    <xs:complexContent mixed="false">
      <xs:extension base="BaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Configuration" type="Configuration" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="BaseRQ">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="echoToken" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="timeoutMilliseconds" type="xs:int" />
      <xs:element minOccurs="0" maxOccurs="1" name="source" type="Source" />
      <xs:element minOccurs="0" maxOccurs="1" name="filterAuditData" type="FilterAuditData" />
	  <xs:element minOccurs="1" maxOccurs="1" name="optionsQuota" type="xs:int" />
	  <xs:element minOccurs="0" maxOccurs="1" name="ContinuationToken" type="ContinuationToken" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Source">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="agencyCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="languageCode" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="FilterAuditData">
    <xs:sequence>
      <xs:element minOccurs="1" maxOccurs="1" name="registerTransactions" type="xs:boolean" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ContinuationToken">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="expectedRange" type="xs:int"/>
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>  
  <xs:complexType name="Configuration">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="User" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Password" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UrlAvail" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UrlReservation" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UrlValuation" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UrlGeneric" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Parameters">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Parameter" type="Parameter" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Parameter">
    <xs:attribute name="key" type="xs:string" />
    <xs:attribute name="value" type="xs:string" />
  </xs:complexType>
  <xs:simpleType name="eTypeSearch">
    <xs:restriction base="xs:string">
	  <xs:enumeration value="MultiRoom" />
      <xs:enumeration value="Combined" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eTypeBusinessRule">
    <xs:restriction base="xs:string">
      <xs:enumeration value="CheaperAmount" />
      <xs:enumeration value="RoomType" />	  
    </xs:restriction>
  </xs:simpleType> 
  <xs:complexType name="AvailDestinations">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Destination" type="Destination" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Destination">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="GeoCode" type="GeoCode" />
    </xs:sequence>
    <xs:attribute name="type" type="eTipoDestino" use="required" />
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="nivelMinimo" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="GeoCode">
    <xs:attribute name="latitude" type="xs:string" />
    <xs:attribute name="longitude" type="xs:string" />
    <xs:attribute name="radiusKm" type="xs:string" />
  </xs:complexType>
  <xs:simpleType name="eTipoDestino">
    <xs:restriction base="xs:string">
      <xs:enumeration value="HOT" />
      <xs:enumeration value="CTY" />
      <xs:enumeration value="ZON" />
      <xs:enumeration value="GEO" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="RoomCandidates">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="RoomCandidate" type="RoomCandidate" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="RoomCandidate">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Paxes" type="Paxes" />
    </xs:sequence>
    <xs:attribute name="id" type="xs:int" use="required" />
  </xs:complexType>
  <xs:complexType name="Paxes">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Pax" type="Pax" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Pax">
    <xs:attribute name="age" type="xs:int" use="required" />
    <xs:attribute name="id" type="xs:int" use="required" />
  </xs:complexType>
  <xs:element name="AvailRS" nillable="true" type="AvailRS" />
  <xs:complexType name="AvailRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Hotels" type="HotelsAvail" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="HotelBaseRS">
    <xs:complexContent mixed="false">
      <xs:extension base="BaseRS" />
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="BaseRS">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="echoToken" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="auditData" type="AuditData" />
      <xs:element minOccurs="1" maxOccurs="1" name="operationImplemented" type="xs:boolean" />
	  <xs:element minOccurs="0" maxOccurs="1" name="ContinuationToken" type="ContinuationToken" />	  
      <xs:element minOccurs="0" maxOccurs="unbounded" name="applicationErrors" type="ApplicationError" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="AuditData">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="transactions" type="Transaction" />
      <xs:element minOccurs="1" maxOccurs="1" name="timeStamp" type="xs:dateTime" />
      <xs:element minOccurs="1" maxOccurs="1" name="processTimeMilliseconds" type="xs:int" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Transaction">
    <xs:sequence>
      <xs:element minOccurs="1" maxOccurs="1" name="timeStamp" type="xs:dateTime" />
      <xs:element minOccurs="0" maxOccurs="1" name="RQ" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="RS" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ApplicationError">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="code" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="type" type="xs:int" />
      <xs:element minOccurs="0" maxOccurs="1" name="description" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="HotelsAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Hotel" type="HotelAvail" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="HotelAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="MealPlans" type="MealPlansAvail" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="MealPlansAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="MealPlan" type="MealPlanAvail" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="MealPlanAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Options" type="Options" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="Options">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Option" type="Option" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Option">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="RoomsAvail" />
      <xs:element minOccurs="0" maxOccurs="1" name="RateRules" type="RateRules" />
      <xs:element minOccurs="0" maxOccurs="1" name="Detail" type="Detail" />
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
      <xs:element minOccurs="0" maxOccurs="1" name="Fees" type="Fees" />
      <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
      <xs:element minOccurs="0" maxOccurs="1" name="CancelPenalties" type="CancelPenalties" />
	  <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="Remarks" />
	  <xs:element minOccurs="0" maxOccurs="1" name="Offers" type="Offers" />
    </xs:sequence>
    <xs:attribute name="supplierCode" type="xs:string" />
    <xs:attribute name="type" type="eTipoOpcion" use="required" />
    <xs:attribute name="paymentType" type="eTipoFormaPago" use="required" />
    <xs:attribute name="status" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="RoomsAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Room" type="RoomAvail" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="RoomAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
	  <xs:element minOccurs="0" maxOccurs="1" name="Beds" type="Beds" />	  
      <xs:element minOccurs="0" maxOccurs="1" name="DailyPrices" type="ArrayOfDailyPrice" />
	  <xs:element minOccurs="0" maxOccurs="1" name="DailyRatePlans" type="ArrayOfDailyRatePlan" />	  
	  <xs:element minOccurs="0" maxOccurs="1" name="Features" type="Features" />	  
    </xs:sequence>
    <xs:attribute name="id" type="xs:string" />
    <xs:attribute name="roomCandidateRefId" type="xs:int" use="required" />
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="description" type="xs:string" />
    <xs:attribute name="nonRefundable" type="xs:boolean" />
  </xs:complexType>
  <xs:complexType name="Price">
    <xs:attribute name="currency" type="xs:string" />
    <xs:attribute name="amount" type="xs:decimal" use="required" />
    <xs:attribute name="binding" type="xs:boolean" use="required" />
    <xs:attribute name="commission" type="xs:decimal" use="required" />
  </xs:complexType>
  <xs:complexType name="Beds">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Bed" type="Bed" />
    </xs:sequence>
	<xs:attribute name="sharedBed" type="xs:boolean" />
  </xs:complexType> 
   <xs:complexType name="Bed">
    <xs:attribute name="numberOfBeds" type="xs:string" />
	<xs:attribute name="type" type="xs:string" />
  </xs:complexType>   
  <xs:complexType name="ArrayOfDailyPrice">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="DailyPrice" nillable="true" type="DailyPrice" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="DailyPrice">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
    </xs:sequence>
    <xs:attribute name="effectiveDate" type="xs:string" />
    <xs:attribute name="expireDate" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="ArrayOfDailyRatePlan">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="DailyRatePlan" nillable="true" type="DailyRatePlan" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="DailyRatePlan">
    <xs:attribute name="effectiveDate" type="xs:string" />
    <xs:attribute name="expireDate" type="xs:string" />
	<xs:attribute name="code" type="xs:string" />
  </xs:complexType>  
  <xs:complexType name="Features">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Feature" type="Feature" />
    </xs:sequence>
  </xs:complexType>
   <xs:complexType name="Feature">
    <xs:attribute name="code" type="xs:string" />
  </xs:complexType>  
  <xs:complexType name="RateRules">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Rules" type="ArrayOfCRule" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ArrayOfCRule">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Rule" nillable="true" type="Rule" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Rule">
    <xs:attribute name="type" type="eTipoCondicionTarifa" use="required" />
  </xs:complexType>
  <xs:simpleType name="eTipoCondicionTarifa">
    <xs:restriction base="xs:string">
      <xs:enumeration value="NonRefundable" />
      <xs:enumeration value="Older55" />
      <xs:enumeration value="Older60" />
      <xs:enumeration value="Older65" />
      <xs:enumeration value="Package" />
      <xs:enumeration value="CanaryResident" />
      <xs:enumeration value="BalearicResident" />
      <xs:enumeration value="largeFamily" />
      <xs:enumeration value="honeymoon" />	  
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="RangeDates">
    <xs:attribute name="startDate" type="xs:string" />
    <xs:attribute name="endDate" type="xs:string" />
  </xs:complexType>
  <xs:simpleType name="durationType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Range" />
      <xs:enumeration value="Open" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="unit">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Day" />
      <xs:enumeration value="Hour" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="Detail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="POIs" type="ArrayOfPOIDetail" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ArrayOfPOIDetail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="POI" nillable="true" type="POIDetail" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="POIDetail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Services" type="ArrayOfService" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="Description" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="ArrayOfService">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Service" nillable="true" type="Service" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Service">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="RangeDates" type="RangeDates" />
    </xs:sequence>
    <xs:attribute name="type" type="eTipoServicio" use="required" />
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="description" type="xs:string" />
    <xs:attribute name="durationType" type="durationType" use="required" />
    <xs:attribute name="quantity" type="xs:int" use="required" />
    <xs:attribute name="unit" type="unit" use="required" />
  </xs:complexType>
  <xs:simpleType name="eTipoServicio">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Null" />
      <xs:enumeration value="SkiPass" />
      <xs:enumeration value="Lessons" />
      <xs:enumeration value="Meals" />
      <xs:enumeration value="Equipment" />
      <xs:enumeration value="Ticket" />
      <xs:enumeration value="Transfers" />
      <xs:enumeration value="Gala" />
      <xs:enumeration value="Activity" />	  	  
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="Fees">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Fee" type="Fee" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Fee">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
    </xs:sequence>
    <xs:attribute name="includedPriceOption" type="xs:boolean" use="required" />
    <xs:attribute name="description" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="CancelPenalties">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="CancelPenalty" type="CancelPenalty" />
    </xs:sequence>
    <xs:attribute name="nonRefundable" type="xs:boolean" use="required" />
  </xs:complexType>
  <xs:complexType name="CancelPenalty">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="HoursBefore" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Penalty" type="Penalty" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Penalty">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="type" type="xs:string" />
        <xs:attribute name="paymentType" type="eTipoFormaPago" use="required" />
        <xs:attribute name="currency" type="xs:string" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
  <xs:complexType name="AvailableModifications">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="AvailableModification" type="AvailableModification" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="AvailableModification">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="ModificationTypes" type="ModificationTypes" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModificationPenalties" type="ModificationPenalties" />	  
    </xs:sequence>
  </xs:complexType>
   <xs:complexType name="ModificationTypes">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="ModificationType" type="eTypeModify" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Remarks">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Remark" type="Remark" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ModificationPenalties">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="ModificationPenalty" type="ModificationPenalty" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ModificationPenalty">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="HoursBefore" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Penalty" type="Penalty" />
    </xs:sequence>
     <xs:attribute name="allowed" type="xs:boolean" use ="required" />		
  </xs:complexType>
   <xs:complexType name="Remark">
    <xs:simpleContent>
      <xs:extension base="xs:string">
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
  <xs:simpleType name="eTipoFormaPago">
    <xs:restriction base="xs:string">
      <xs:enumeration value="LaterPay" />
      <xs:enumeration value="MerchantPay" />
      <xs:enumeration value="MixedPay" />
	  <xs:enumeration value="CardBookingPay" />
	  <xs:enumeration value="CardCheckInPay" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eTipoOpcion">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Hotel" />
      <xs:enumeration value="HotelSkiPass" />
      <xs:enumeration value="HotelSkiPassLessons" />
      <xs:enumeration value="HotelSkiPassLessonsMeals" />
      <xs:enumeration value="HotelSkiPassEquipmentLessons" />
      <xs:enumeration value="HotelSkiPassEquipmentLessonsMeals" />
      <xs:enumeration value="HotelTicket" />
      <xs:enumeration value="HotelTicketTransfers" />
      <xs:enumeration value="Gala" />
      <xs:enumeration value="HotelSkiPassEquipment" />
      <xs:enumeration value="HotelSkiPassMeals" />
      <xs:enumeration value="HotelSkiPassEquipmentMeals" />
      <xs:enumeration value="HotelActivity" />	  
    </xs:restriction>
  </xs:simpleType>
   <xs:complexType name="Offers">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Offer" type="Offer" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Offer">
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
  </xs:complexType>
    <xs:element name="ValuationRQ" nillable="true" type="ValuationRQ" />
    <xs:complexType name="ValuationRQ">
      <xs:complexContent mixed="false">
        <xs:extension base="HotelBaseRQ">
          <xs:sequence>
            <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
            <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
            <xs:element minOccurs="0" maxOccurs="1" name="SupplierCode" type="xs:string" />
			<xs:element minOccurs="1" maxOccurs="1" name="OnRequest" type="xs:boolean" />
            <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
            <xs:element minOccurs="0" maxOccurs="1" name="MealPlanCode" type="xs:string" />
            <xs:element minOccurs="0" maxOccurs="1" name="HotelCode" type="xs:string" />
            <xs:element minOccurs="1" maxOccurs="1" name="PaymentType" type="eTipoFormaPago" />
            <xs:element minOccurs="1" maxOccurs="1" name="OptionType" type="eTipoOpcion" />
	        <xs:element minOccurs="0" maxOccurs="1" name="BlockOption" type="xs:boolean" />	
            <xs:element minOccurs="0" maxOccurs="1" name="Nationality" type="xs:string" />				
            <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="RoomsAvail" />
            <xs:element minOccurs="0" maxOccurs="1" name="RoomCandidates" type="RoomCandidates" />
          </xs:sequence>
        </xs:extension>
      </xs:complexContent>
    </xs:complexType>

    <xs:element name="ValuationRS" nillable="true" type="ValuationRS" />
    <xs:complexType name="ValuationRS">
      <xs:complexContent mixed="false">
        <xs:extension base="HotelBaseRS">
          <xs:sequence>
            <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
		    <xs:element minOccurs="1" maxOccurs="1" name="Status" type="eEstadoReserva" />
            <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
            <xs:element minOccurs="0" maxOccurs="1" name="Fees" type="Fees" />
            <xs:element minOccurs="0" maxOccurs="1" name="CancelPenalties" type="CancelPenalties" />
            <xs:element minOccurs="0" maxOccurs="1" name="AvailableModifications" type="AvailableModifications" />			
            <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="xs:string" />
	        <xs:element minOccurs="0" maxOccurs="1" name="Offers" type="Offers" />
            <xs:element minOccurs="0" maxOccurs="1" name="PaymentOptions" type="PaymentOptions" />
            <xs:element minOccurs="0" maxOccurs="1" name="Option" type="Option" />
            <xs:element minOccurs="0" maxOccurs="1" name="CancelPoliciesDescription" type="xs:string" />			
          </xs:sequence>
        </xs:extension>
      </xs:complexContent>
    </xs:complexType>
   
    <xs:complexType name="PaymentOptions">
      <xs:sequence>
        <xs:element minOccurs="0" maxOccurs="1" name="Cards" type="ArrayOfCard" />
      </xs:sequence>
      <xs:attribute name="cash" type="xs:boolean" use="required" />
      <xs:attribute name="bankAcct" type="xs:boolean" use="required" />
    </xs:complexType>
    <xs:complexType name="ArrayOfCard">
      <xs:sequence>
        <xs:element minOccurs="0" maxOccurs="unbounded" name="Card" nillable="true" type="Card" />
      </xs:sequence>
    </xs:complexType>
    <xs:complexType name="Card">
      <xs:attribute name="code" type="eCodeCard" use="required" />
    </xs:complexType>
    <xs:simpleType name="eCodeCard">
      <xs:restriction base="xs:string">
        <xs:enumeration value="VI" />
        <xs:enumeration value="AX" />
        <xs:enumeration value="BC" />
        <xs:enumeration value="CA" />
        <xs:enumeration value="CB" />
        <xs:enumeration value="CU" />
        <xs:enumeration value="DS" />
        <xs:enumeration value="DC" />
        <xs:enumeration value="T" />
        <xs:enumeration value="R" />
        <xs:enumeration value="N" />
        <xs:enumeration value="L" />
        <xs:enumeration value="E" />
        <xs:enumeration value="JC" />
        <xs:enumeration value="TO" />
        <xs:enumeration value="S" />
        <xs:enumeration value="EC" />
        <xs:enumeration value="EU" />
        <xs:enumeration value="TP" />
        <xs:enumeration value="OP" />
        <xs:enumeration value="ER" />
        <xs:enumeration value="XS" />
        <xs:enumeration value="O" />
      </xs:restriction>
    </xs:simpleType>

  <xs:element name="ReservationRQ" nillable="true" type="ReservationRQ" />
  <xs:complexType name="ReservationRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="ClientLocator" type="xs:string" />
		  <xs:element minOccurs="1" maxOccurs="1" name="OnRequest" type="xs:boolean" />
          <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
          <xs:element minOccurs="0" maxOccurs="1" name="DeltaPrice" type="DeltaPrice" />
          <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="MarcaExterna" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="MealPlanCode" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
          <xs:element minOccurs="0" maxOccurs="1" name="ResGuests" type="ResGuests" />
          <xs:element minOccurs="1" maxOccurs="1" name="PaymentType" type="eTipoFormaPago" />
          <xs:element minOccurs="0" maxOccurs="1" name="CardInfo" type="CardInfo" />
          <xs:element minOccurs="0" maxOccurs="1" name="HotelCode" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="RoomsAvail" />
          <xs:element minOccurs="0" maxOccurs="1" name="RoomCandidates" type="RoomCandidates" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="DeltaPrice">
    <xs:attribute name="amount" type="xs:string" />
    <xs:attribute name="percent" type="xs:string" />
    <xs:attribute name="applyBoth" type="xs:boolean" use="required" />
  </xs:complexType>
  <xs:complexType name="ResGuests">
    <xs:sequence>	
      <xs:element minOccurs="0" maxOccurs="1" name="Guests" type="Guests" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Guests">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Guest" type="Guest" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Guest">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="GivenName" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="SurName" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Telephone" type="xs:string" />
    </xs:sequence>
    <xs:attribute name="roomCandidateId" type="xs:int" use="required" />
    <xs:attribute name="paxId" type="xs:int" use="required" />
  </xs:complexType> 
  <xs:complexType name="CardInfo">
    <xs:sequence>
      <xs:element minOccurs="1" maxOccurs="1" name="CardCode" type="eCodeCard" />
      <xs:element minOccurs="0" maxOccurs="1" name="Number" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Holder" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ValidityDate" type="ValidityDate" />
      <xs:element minOccurs="0" maxOccurs="1" name="CVC" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ValidityDate">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Month" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Year" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:element name="ReservationRS" nillable="true" type="ReservationRS" />
  <xs:complexType name="ReservationRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="ProviderLocator" type="xs:string" />
          <xs:element minOccurs="1" maxOccurs="1" name="ResStatus" type="eEstadoReserva" />
          <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
          <xs:element minOccurs="0" maxOccurs="1" name="BillingSupplierCode" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Payable" type="Payable" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:simpleType name="eEstadoReserva">
    <xs:restriction base="xs:string">
      <xs:enumeration value="RQ" />
      <xs:enumeration value="OK" />
      <xs:enumeration value="CN" />
      <xs:enumeration value="UN" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="Payable">
    <xs:attribute name="value" type="xs:string" />
  </xs:complexType>
  <xs:element name="ReservationReadRQ" nillable="true" type="ReservationReadRQ" />
  <xs:complexType name="ReservationReadRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Locators" type="Locators" />
          <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="CreationDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Currency" type="xs:string" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Locators">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Client" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Provider" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:element name="ReservationReadRS" nillable="true" type="ReservationReadRS" />
  <xs:complexType name="ReservationReadRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Locators" type="Locators" />
          <xs:element minOccurs="1" maxOccurs="1" name="TypePrice" type="eTypePrice" />
          <xs:element minOccurs="0" maxOccurs="1" name="Hotel" type="HotelRes" />
          <xs:element minOccurs="0" maxOccurs="1" name="TransactionStatus" type="TransactionStatus" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:simpleType name="eTypePrice">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Real" />
      <xs:enumeration value="BindingPriceWithoutInformedCommission" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="HotelRes">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="City" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="CreationDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="MealPlanCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Holder" type="Holder" />
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
      <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="RoomsAvail" />
      <xs:element minOccurs="0" maxOccurs="1" name="RoomCandidates" type="RoomCandidates" />
      <xs:element minOccurs="0" maxOccurs="1" name="CancelPenalties" type="CancelPenalties" />
	  <xs:element minOccurs="0" maxOccurs="1" name="PaymentOptions" type="PaymentOptions" />
      <xs:element minOccurs="0" maxOccurs="1" name="AvailableModifications" type="AvailableModifications" />		  
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Holder">
    <xs:attribute name="name" type="xs:string" />
    <xs:attribute name="surname" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="TransactionStatus">
    <xs:sequence>
      <xs:element minOccurs="1" maxOccurs="1" name="ComunicationStatus" type="eEstadoComunicacion" />
      <xs:element minOccurs="1" maxOccurs="1" name="RSStatus" type="eEstadoRespuesta" />
      <xs:element minOccurs="1" maxOccurs="1" name="ResStatus" type="eEstadoReserva" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="eEstadoComunicacion">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OFFLINE" />
      <xs:enumeration value="KO" />
      <xs:enumeration value="OK" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eEstadoRespuesta">
    <xs:restriction base="xs:string">
      <xs:enumeration value="DESCONOCIDO" />
      <xs:enumeration value="EXISTE" />
      <xs:enumeration value="EXISTECANCELADA" />
      <xs:enumeration value="NO_EXISTE" />
    </xs:restriction>
  </xs:simpleType>
  <xs:element name="ReservationListRQ" nillable="true" type="ReservationListRQ" />
  <xs:complexType name="ReservationListRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Currency" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Start" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="End" type="xs:string" />
          <xs:element minOccurs="1" maxOccurs="1" name="DateType" type="eTipoFecha" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:simpleType name="eTipoFecha">
    <xs:restriction base="xs:string">
      <xs:enumeration value="B" />
      <xs:enumeration value="A" />
    </xs:restriction>
  </xs:simpleType>
  
   <xs:element name="ReservationListRS" nillable="true" type="ReservationListRS" />
  <xs:complexType name="ReservationListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Reservations" type="Reservations" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  
  <xs:complexType name="Reservations">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Reservation" type="ReservationReadRS" />
    </xs:sequence>
  </xs:complexType>
<xs:element name="CancelRQ" nillable="true" type="CancelRQ" />
  <xs:complexType name="CancelRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Locators" type="Locators" />
          <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Currency" type="xs:string" />
        </xs:sequence>
        <xs:attribute name="hotelCode" type="xs:string" />
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="CancelRS" nillable="true" type="CancelRS" />
  <xs:complexType name="CancelRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="ProviderLocator" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="CancelId" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="xs:string" />
          <xs:element minOccurs="0" maxOccurs="1" name="TransactionStatus" type="TransactionStatus" />
          <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  



 <xs:element name="HotelListRQ" nillable="true" type="HotelListRQ" />
  <xs:complexType name="HotelListRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ"/>
    </xs:complexContent>
  </xs:complexType>
  
  <xs:element name="CategoryListRQ" nillable="true" type="CategoryListRQ" />
  <xs:complexType name="CategoryListRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  
<xs:element name="DescriptiveInfoRQ" nillable="true" type="DescriptiveInfoRQ" />
  <xs:complexType name="DescriptiveInfoRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Hotel" type="CodeD" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  
 <xs:complexType name="CodeD">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  
 <xs:element name="MealPlanListRQ" nillable="true" type="MealPlanListRQ" />
  <xs:complexType name="MealPlanListRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="GeographicDestinationTreeRQ" nillable="true" type="GeographicDestinationTreeRQ" />
  <xs:complexType name="GeographicDestinationTreeRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
   <xs:element name="RoomListRQ" nillable="true" type="RoomListRQ" />
  <xs:complexType name="RoomListRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  
 <xs:element name="AvailDestinationTreeRQ" nillable="true" type="AvailDestinationTreeRQ" />
  <xs:complexType name="AvailDestinationTreeRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  
 <xs:element name="RuntimeConfigurationRQ" nillable="true" type="RuntimeConfigurationRQ" />
  <xs:complexType name="RuntimeConfigurationRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  
   <xs:element name="StaticConfigurationRQ" nillable="true" type="StaticConfigurationRQ" />
  <xs:complexType name="StaticConfigurationRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ" />
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="MealPlanListRS" nillable="true" type="MealPlanListRS" />
  <xs:complexType name="MealPlanListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="MealPlans" type="MealPlans" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="MealPlans">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="MealPlan" type="MealPlan" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="MealPlan">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
    </xs:sequence>
  </xs:complexType>

  <xs:element name="RoomListRS" nillable="true" type="RoomListRS" />
  <xs:complexType name="RoomListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="RoomsInfo" type="RoomsInfo" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="RoomsInfo">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="RoomInfo" type="RoomInfo" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="RoomInfo">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Language" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
    </xs:sequence>
  </xs:complexType>

  <xs:element name="RuntimeConfigurationRS" nillable="true" type="RuntimeConfigurationRS" />
  <xs:complexType name="RuntimeConfigurationRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Configuration" type="Configuration" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:element name="GeographicDestinationTreeRS" nillable="true" type="GeographicDestinationTreeRS" />
  <xs:complexType name="GeographicDestinationTreeRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="DestinationTree" type="DestinationTreeGeographic" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="DestinationTreeGeographic">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="DestinationLeaf" type="DestinationLeaf" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
    <xs:attribute name="avail" type="xs:boolean" use="required" />
  </xs:complexType>
  <xs:complexType name="DestinationLeaf">
    <xs:attribute name="code" type="xs:string" />
  </xs:complexType>

  <xs:element name="AvailDestinationTreeRS" nillable="true" type="AvailDestinationTreeRS" />
  <xs:complexType name="AvailDestinationTreeRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="DestinationTree" type="DestinationTreeAvail" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="DestinationTreeAvail">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="DestinationLeaf" type="DestinationLeaf" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
  </xs:complexType>

  <xs:element name="DescriptiveInfoRS" nillable="true" type="DescriptiveInfoRS" />
  <xs:complexType name="DescriptiveInfoRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="1" maxOccurs="1" name="UpgradeUTCDate" type="xs:dateTime" />
          <xs:element minOccurs="0" maxOccurs="1" name="Hotel" type="Hotel" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Hotel">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="GiataId" type="GiataId" />
      <xs:element minOccurs="0" maxOccurs="1" name="GiataFormatCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Address" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Town" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ZipCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="CountryISOCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="AvailDestination" type="DestinationTreeAvail" />
      <xs:element minOccurs="0" maxOccurs="1" name="GeographicDestination" type="DestinationTreeGeographic" />
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Contact" type="ContactInfo" />
      <xs:element minOccurs="0" maxOccurs="1" name="BookingContact" type="ContactInfo" />
      <xs:element minOccurs="0" maxOccurs="1" name="CategoryCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Type" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ChainCode" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ShortDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="LongDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="HowToGet" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="RoomsDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="SituationDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="RestaurantsDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="PoolsDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ActivitiesDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="ServicesDescription" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="AdditionalDetails" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Attributes" type="Attributes" />
      <xs:element minOccurs="0" maxOccurs="1" name="Images" type="Images" />
      <xs:element minOccurs="0" maxOccurs="1" name="LocationType" type="LocationType" />
      <xs:element minOccurs="0" maxOccurs="1" name="Typologies" type="ArrayOfString" />
      <xs:element minOccurs="0" maxOccurs="1" name="RenovationYear" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="PaymentOptions" type="PaymentOptions" />
      <xs:element minOccurs="0" maxOccurs="1" name="ExclusiveDeal" type="xs:boolean" />	  
      <xs:element minOccurs="0" maxOccurs="1" name="AreaInfo" type="AreaInfo" />
      <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="ArrayOfRoom" />
	  <xs:element minOccurs="0" maxOccurs="1" name="PropertyCategory" type="PropertyCategory" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="GiataId">
    <xs:simpleContent>
      <xs:extension base="xs:string">
	  	<xs:attribute name="source" type="xs:string" />
      </xs:extension>  
    </xs:simpleContent>
  </xs:complexType>   
  <xs:complexType name="ContactInfo">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Email" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Telephone" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Fax" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Web" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Attributes">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Attribute" type="Attribute" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Attribute">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Value" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Classification" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Images">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Picture" type="Picture" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Picture">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="URL" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Classification" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Ordered" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="LocationType">
    <xs:sequence>
      <xs:element minOccurs="1" maxOccurs="1" name="Type" type="eTipoLocalizacion" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="eTipoLocalizacion">
    <xs:restriction base="xs:string">
      <xs:enumeration value="None" />
      <xs:enumeration value="City" />
      <xs:enumeration value="Rural" />
      <xs:enumeration value="Beach" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="ArrayOfString">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Typology" nillable="true" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="AreaInfo">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Atractions" type="ArrayOfAtraction" />
      <xs:element minOccurs="0" maxOccurs="1" name="Recreations" type="ArrayOfRecreation" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ArrayOfAtraction">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Atraction" nillable="true" type="Atraction" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Atraction">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Address" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Contact" type="ContactInfo" />
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Schedules" type="ArrayOfSchedule" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
    <xs:attribute name="type" type="eTypeAtraction" use="required" />
    <xs:attribute name="proximityType" type="eTypeProximity" use="required" />
  </xs:complexType>
  <xs:complexType name="ArrayOfSchedule">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Schedule" nillable="true" type="Schedule" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Schedule">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Charge" type="Charge" />
    </xs:sequence>
    <xs:attribute name="name" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="Charge">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="eTypeAtraction">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Restaurant" />
      <xs:enumeration value="Casino" />
      <xs:enumeration value="Bar" />
      <xs:enumeration value="Others" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eTypeProximity">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnSite" />
      <xs:enumeration value="OffSite" />
      <xs:enumeration value="Nearby" />
      <xs:enumeration value="NotAvailable" />
      <xs:enumeration value="OnOffSite" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="ArrayOfRecreation">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Recreation" nillable="true" type="Recreation" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Recreation">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Address" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Contact" type="ContactInfo" />
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:string" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="name" type="xs:string" />
    <xs:attribute name="included" type="xs:boolean" use="required" />
    <xs:attribute name="proximityType" type="eTypeProximity" use="required" />
  </xs:complexType>
  <xs:complexType name="ArrayOfRoom">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Room" nillable="true" type="Room" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Room">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Attributes" type="Attributes" />
      <xs:element minOccurs="0" maxOccurs="1" name="Images" type="Images" />
      <xs:element minOccurs="0" maxOccurs="1" name="Description" type="xs:string" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
    <xs:attribute name="size" type="xs:int" use="required" />
    <xs:attribute name="quantity" type="xs:int" use="required" />
    <xs:attribute name="viewCode" type="eViewCode" use="required" />
    <xs:attribute name="classificationCode" type="eRoomClassificacionCode" use="required" />
    <xs:attribute name="occupancy" type="xs:int" use="required" />
  </xs:complexType>
  <xs:simpleType name="eViewCode">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Airport" />
      <xs:enumeration value="Mountain" />
      <xs:enumeration value="Ocean" />
      <xs:enumeration value="Pool" />
      <xs:enumeration value="River" />
      <xs:enumeration value="Water" />
      <xs:enumeration value="Beach" />
      <xs:enumeration value="Garden" />
      <xs:enumeration value="Park" />
      <xs:enumeration value="Forest" />
      <xs:enumeration value="RainForest" />
      <xs:enumeration value="Bay" />
      <xs:enumeration value="Countryside" />
      <xs:enumeration value="Sea" />
      <xs:enumeration value="Golf" />
      <xs:enumeration value="Various" />
      <xs:enumeration value="Others" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eRoomClassificacionCode">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Aparments" />
      <xs:enumeration value="Studios" />
      <xs:enumeration value="Classic" />
      <xs:enumeration value="Comfort" />
      <xs:enumeration value="Deluxe" />
      <xs:enumeration value="DeluxeSuite" />
      <xs:enumeration value="Economy" />
      <xs:enumeration value="Luxury" />
      <xs:enumeration value="Premier" />
      <xs:enumeration value="Standard" />
      <xs:enumeration value="Superior" />
      <xs:enumeration value="JuniorSuite" />
      <xs:enumeration value="Bungalow" />
      <xs:enumeration value="Cottage" />
      <xs:enumeration value="House" />
      <xs:enumeration value="AllEstablishment" />
      <xs:enumeration value="Aparthotel" />
      <xs:enumeration value="Cave" />
      <xs:enumeration value="Plaza" />
      <xs:enumeration value="Bed" />
      <xs:enumeration value="Others" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="PropertyCategory">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />	  
    </xs:sequence>
  </xs:complexType>
  <xs:element name="CategoryListRS" nillable="true" type="CategoryListRS" />
  <xs:complexType name="CategoryListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Categories" type="Categories" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  
  <xs:complexType name="Categories">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Category" type="Category" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Category">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
   <xs:element name="StaticConfigurationRS" nillable="true" type="StaticConfigurationRS" />
  <xs:complexType name="StaticConfigurationRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="1" maxOccurs="1" name="MaxNumberHotels" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="MaxNumberCities" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="MaxNumberZones" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="MaxNumberGeoCodes" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="RequiredRoomList" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformCancelPolicies" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformBindingPriceValuation" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformBindingPrice" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformNRFValuation" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformNRFRate" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="Inform55Rate" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformPackageRate" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformExtraActivity" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformForfait" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="RemarksValuation" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="MaxNumberRoomCandidates" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="MaxPaxInRoomCandidates" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="Release" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="MinimumStay" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformBillingSupplierReservation" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="ImplementsProvideLocatorReservationRead" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="ImplementsClientLocatorReservationRead" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="ImplementsCancel" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformPriceReservation" type="xs:boolean" />
          <xs:element minOccurs="0" maxOccurs="1" name="HotelListLanguages" type="HotelListLanguages" />
          <xs:element minOccurs="1" maxOccurs="1" name="ReservationListCreationDate" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="ReservationListCheckDate" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="HotelListType" type="eListado" />
          <xs:element minOccurs="1" maxOccurs="1" name="DescriptiveInfoType" type="eInformacion" />
          <xs:element minOccurs="1" maxOccurs="1" name="GeographicDestinationTreeType" type="eArbolGeografico" />
          <xs:element minOccurs="1" maxOccurs="1" name="AvailDestinationTreeType" type="eArbolDestinos" />
          <xs:element minOccurs="1" maxOccurs="1" name="ListadoServicios" type="eTypeListado" />
          <xs:element minOccurs="1" maxOccurs="1" name="RoomListType" type="eTypeListado" />
          <xs:element minOccurs="1" maxOccurs="1" name="DescriptiveInfoParallelism" type="xs:int" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformCancelPoliciesReservationRead" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformCancelPoliciesReservationList" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformCancelPoliciesAvail" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="InformChangesPolicies" type="xs:boolean" />
          <xs:element minOccurs="1" maxOccurs="1" name="ImplementsDeltaPrice" type="xs:boolean" />
		  <xs:element minOccurs="1" maxOccurs="1" name="RequiredAllPassengers" type="xs:boolean" />
          <xs:element minOccurs="0" maxOccurs="1" name="ModifyTransactions" type="ModifyTransactions" />
		  <xs:element minOccurs="1" maxOccurs="1" name="InformNRFRateByRoom" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="CurrencyList" type="CurrencyList" />
		  <xs:element minOccurs="0" maxOccurs="1" name="AllowsCurrencyAvail" type="xs:boolean" />
		  <xs:element minOccurs="1" maxOccurs="1" name="SearchTypeMultiRoom" type="xs:boolean" />
		  <xs:element minOccurs="1" maxOccurs="1" name="InformCancelPoliciesModify" type="xs:boolean" />
		  <xs:element minOccurs="1" maxOccurs="1" name="AllowOnRequest" type="xs:boolean" />		  
		  <xs:element minOccurs="0" maxOccurs="1" name="ImplementsDailyRatePlan" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="AllowRemarks" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="InformSharedBed" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="InformBedType" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="InformNumberOfBeds" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="AllowBlockOption" type="xs:boolean" />		
		  <xs:element minOccurs="0" maxOccurs="1" name="InformExclusiveDeal" type="xs:boolean" />	
		  <xs:element minOccurs="0" maxOccurs="1" name="InformPriceCancel" type="xs:boolean" />	
		  <xs:element minOccurs="0" maxOccurs="1" name="AllowUrlCard" type="xs:boolean" />		
		  <xs:element minOccurs="0" maxOccurs="1" name="InformCancelPoliciesDescription" type="xs:boolean" />
		  <xs:element minOccurs="0" maxOccurs="1" name="PaymentTypes" type="PaymentTypes" />
          <xs:element minOccurs="0" maxOccurs="1" name="ImplementsBusinessRules" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="InformAvailableModificationsInReservationRead" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="RequiredNationality" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="Inform60Rate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="Inform65Rate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="InformCanaryResidentRate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="InformBalearicResidentRate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="InformLargeFamilyRate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="InformHoneymoonRate" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="ImplementsProviderLocatorCancel" type="xs:boolean" />	
          <xs:element minOccurs="0" maxOccurs="1" name="ImplementsClientLocatorCancel" type="xs:boolean" />		  
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="ModifyTransactions">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="ModifyTransaction" type="ModifyTransaction" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="ModifyTransaction">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Modify"  type="eTypeModify" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="eTypeModify">
    <xs:restriction base="xs:string">
      <xs:enumeration value="Null" />
      <xs:enumeration value="ModifyStartDateAddDays" />
      <xs:enumeration value="ModifyStartDateSubtractDays" />
      <xs:enumeration value="ModifyEndDateAddDays" />
      <xs:enumeration value="ModifyEndDateSubtractDays" />
      <xs:enumeration value="ModifyHolder" />
      <xs:enumeration value="ModifyRoomsAddRooms" />
      <xs:enumeration value="ModifyRoomsRemoveRooms" />
	  <xs:enumeration value="ModifyMealPlan" />
	  <xs:enumeration value="ModifyAddComment" />
    </xs:restriction>
  </xs:simpleType>
  
  <xs:complexType name="PaymentTypes">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="PaymentType" type="eTipoFormaPago" />
    </xs:sequence>
  </xs:complexType>
  
 <xs:complexType name="HotelListLanguages">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Languages" type="Languages" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Languages">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Language" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
    <xs:complexType name="CurrencyList">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="CurrencyCode" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="eListado">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnLine" />
      <xs:enumeration value="OffLine" />
      <xs:enumeration value="OffLineCompleted" />
      <xs:enumeration value="OnLineCompleted" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eInformacion">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnLine" />
      <xs:enumeration value="OffLine" />
      <xs:enumeration value="NotImplemented" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eArbolGeografico">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnLine" />
      <xs:enumeration value="OffLine" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eArbolDestinos">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnLine" />
      <xs:enumeration value="OffLine" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="eTypeListado">
    <xs:restriction base="xs:string">
      <xs:enumeration value="OnLine" />
      <xs:enumeration value="OffLine" />
    </xs:restriction>
  </xs:simpleType>
 <xs:element name="HotelListRS" nillable="true" type="HotelListRS" />
  <xs:complexType name="HotelListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="1" maxOccurs="1" name="UpgradeUTCDate" type="xs:dateTime" />
          <xs:element minOccurs="0" maxOccurs="1" name="Hotels" type="Hotels" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Hotels">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Hotel" type="Hotel" />
    </xs:sequence>
  </xs:complexType>
  <xs:element name="ModifyValuationRQ" type="ModifyValuationRQ" />
  <xs:complexType name="ModifyValuationRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
	      <xs:element minOccurs="0" maxOccurs="1" name="OnRequest" type="xs:boolean" />
          <xs:element minOccurs="0" maxOccurs="1" name="Nationality" type="xs:string" />		  
	      <xs:element minOccurs="0" maxOccurs="1" name="BlockOption" type="xs:boolean" />	 		  
          <xs:element minOccurs="0" maxOccurs="1" name="Reservation" type="Reservation" />
          <xs:element minOccurs="0" maxOccurs="1" name="Modifications" type="Modifications" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Reservation">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Locators" type="Locators" /> 
      <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="CreationDate" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Currency" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Modifications">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyStartDateAddDays" type="StartDate" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyStartDateSubtractDays" type="StartDate" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyEndDateAddDays" type="EndDate" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyEndDateSubtractDays" type="EndDate" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyHolder" type="ModifyHolder" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyRoomsAddRooms" type="ModifyRoomsAddRooms" />
      <xs:element minOccurs="0" maxOccurs="1" name="ModifyRoomsRemoveRooms" type="ModifyRoomsRemoveRooms" />
	  <xs:element minOccurs="0" maxOccurs="1" name="ModifyMealPlan" type="ModifyMealPlan" />
	  <xs:element minOccurs="0" maxOccurs="1" name="ModifyAddComment" type="ModifyAddComment" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="StartDate">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="StartDate" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="EndDate">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="EndDate" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ModifyHolder">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Holder" type="Holder" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ModifyRoomsAddRooms">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="ArrayOfRoomAdd" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ArrayOfRoomAdd">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Room" nillable="true" type="RoomAdd" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="RoomAdd">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="PaxGuests" type="ArrayOfPaxGuest" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="ArrayOfPaxGuest">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="PaxGuest" nillable="true" type="PaxGuest" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="PaxGuest">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="GivenName" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="SurName" type="xs:string" />
    </xs:sequence>
    <xs:attribute name="age" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="ModifyRoomsRemoveRooms">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Rooms" type="ArrayOfRoomRemove" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="ArrayOfRoomRemove">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Room" nillable="true" type="RoomRemove" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="RoomRemove">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
	  <xs:element minOccurs="0" maxOccurs="1" name="PaxGuests" type="ArrayOfPaxGuest" />
    </xs:sequence>
    <xs:attribute name="code" type="xs:string" />
  </xs:complexType>
  <xs:complexType name="ModifyMealPlan">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="MealPlanCode" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
   <xs:complexType name="ModifyAddComment">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Comment" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:element name="ModifyValuationRS" type="ModifyValuationRS" />
  <xs:complexType name="ModifyValuationRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
		  <xs:element minOccurs="0" maxOccurs="1" name="Status" type="eEstadoReserva" />		
          <xs:element minOccurs="0" maxOccurs="1" name="ModifyPenalty" type="Price" />
          <xs:element minOccurs="0" maxOccurs="1" name="HotelReservation" type="HotelRes" />
          <xs:element minOccurs="0" maxOccurs="1" name="CancelPenalties" type="CancelPenalties" />		  
          <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="ModifyReservationRQ" type="ModifyReservationRQ" />
  <xs:complexType name="ModifyReservationRQ">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRQ">
        <xs:sequence>
	      <xs:element minOccurs="0" maxOccurs="1" name="OnRequest" type="xs:boolean" />	 
          <xs:element minOccurs="0" maxOccurs="1" name="Nationality" type="xs:string" />		  
          <xs:element minOccurs="0" maxOccurs="1" name="Reservation" type="Reservation" />
          <xs:element minOccurs="0" maxOccurs="1" name="Modifications" type="Modifications" />
          <xs:element minOccurs="0" maxOccurs="1" name="ModifyPenalty" type="Price" />
          <xs:element minOccurs="0" maxOccurs="1" name="HotelReservation" type="HotelRes" />
		  <xs:element minOccurs="0" maxOccurs="1" name="CardInfo" type="CardInfo" />
          <xs:element minOccurs="0" maxOccurs="1" name="Parameters" type="Parameters" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="ModifyReservationRS" type="ModifyReservationRS" />
  <xs:complexType name="ModifyReservationRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="ProviderLocator" type="xs:string" />
          <xs:element minOccurs="1" maxOccurs="1" name="ResStatus" type="eEstadoReserva" />
          <xs:element minOccurs="0" maxOccurs="1" name="Price" type="Price" />
		  <xs:element minOccurs="0" maxOccurs="1" name="Remarks" type="xs:string" />
		  <xs:element minOccurs="0" maxOccurs="1" name="BillingSupplierCode" type="xs:string" />     
		  <xs:element minOccurs="0" maxOccurs="1" name="Payable" type="Payable" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:element name="CurrencyListRQ" nillable="true" type="CurrencyListRQ" />
    <xs:complexType name="CurrencyListRQ">
      <xs:complexContent mixed="false">
          <xs:extension base="HotelBaseRQ" />
      </xs:complexContent>
    </xs:complexType> 

<xs:element name="CurrencyListRS" nillable="true" type="CurrencyListRS" />
  <xs:complexType name="CurrencyListRS">
    <xs:complexContent mixed="false">
      <xs:extension base="HotelBaseRS">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="1" name="Currencies" type="Currencies" />
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>

  <xs:complexType name="Currencies">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="unbounded" name="Currency" type="Currency" />
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Currency">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Code" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Name" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
</xs:schema>
~~~