# kafka_cdc_replication
kafka cdc DB replication

wal_level = logical
max_wal_senders = 10
max_replication_slots = 10

SHOW wal_level;
SHOW max_replication_slots;

SELECT pg_create_physical_replication_slot('replica_slot_02');
SELECT pg_create_physical_replication_slot('replica_slot_03');
SELECT * FROM pg_replication_slots;


CREATE USER replica_user_02 WITH REPLICATION PASSWORD 'user02';
CREATE USER replica_user_03 WITH REPLICATION PASSWORD 'user03';

GRANT CONNECT ON DATABASE kari TO replica_user_02;
GRANT CONNECT ON DATABASE kari TO replica_user_03;

ALTER TABLE satellites REPLICA IDENTITY USING INDEX satellites_pkey;