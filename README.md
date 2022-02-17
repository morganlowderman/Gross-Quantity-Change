
select APF.Contractnumber, grossquantity, AC.ScheduleQuantity, AC.AppliedQuantity, AC.UnsettledQuantity, AC.SettledQuantity, APF.PricingStatus, APF.PositionLocation, APF.PositionSubLocation,
AC.PriceCode, AC.PriceTypeCode, APF.TradeDate
from allpositionsfinal APF
Left Join Stageagriscontracts AC on RIGHT(AC.contractnumber,7) = RIGHT(APF.contractnumber,7) and APF.OriginalCommoditycode = AC.Commoditycode and APF.originallocationcode = AC.LocationCode
where loaddate = '2022-02-08'
and APF.source = 'AGR'
and APF.exceptionkey like 'AGRCONTGAV%'
--and APF.tradedate = APF.loaddate
and positionlocation = 'flat'
order by pricecode, APF.tradedate





select count (*)
from position.allpositionsfinal
where 1=1
and loaddate = '2022-02-08'
and source = 'AGR'
and exceptionkey like 'AGRCONTGAV%'
and not (positionlocation = 'flat' and positionsublocation = 'priced basis' and tradedate = loaddate and unsettledquantity = 0)
and not (positionlocation = 'spot contracts' and unsettledquantity = 0 and tradedate = loaddate)
