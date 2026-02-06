# Hunters Detections
An attempt to commit detections in Hunters as code, can easily converted to detections in Vega, Panther, etc

Mandatory fields:

start_time, end_time type: timestamp - the begining and end of the event. For simple filter detectors, event_time can be used for both fields. For aggregations over time, these should be the earliest and latest times of the aggregation.

event_ids type: Map[string,string[]]- map of data-types and their related event_ids.

dataflow_ids type: uuid[] - The dataflow IDs of all the events included in the detection. This field will enable Datasource Tagging support for the detector. It is recommended to use the METADATA$DATAFLOW_ID field as value, implemented as follows: ARRAY_CONSTRUCT_COMPACT(METADATA$DATAFLOW_ID) for non-GROUP BY queries and ARRAY_AGG(DISTINCT METADATA$DATAFLOW_ID) for GROUP BY queries.

last_event_insertion_time type: timestamp - the latest ingestion timestamp of all the events included in the detection. This field will enable Hunters to monitor delays for this detector. It is recommended to use the METADATA$INSERTION_TIME field as value, implemented as follows: METADATA$INSERTION_TIME for non-GROUP BY queries, and MAX(METADATA$INSERTION_TIME) for GROUP BY queries.
