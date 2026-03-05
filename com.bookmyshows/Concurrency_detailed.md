1) Using synchronized for critical section
- locks critical section and this will be accessible for only one thread
  But in case of distributed systems, this wont help.

2) Using Distributed Concurrency control
   (i) Optimistic locking   (ii) Pessimistic locking

Transactions :
Transaction helps to achieve integrity, helps to avoid inconsistency in our database.
If all operations are success then only commit to DB else, rollback.

DB Locking :
Helps us to make sure that no other transactions updates the locked row
- Two types of lock exists -
  (i) Shared lock/read lock - can not update the row, but can read it
  (ii) Exclusive lock - other transaction can not even read the row

Isolation level :
Even if multiple transactions are running, what is the level of isolation

Isolation level     Dirty Read Possible     Non repeatable read possible       Phantom read possible
Read uncommitted        Yes                         Yes                             Yes
Read committed          No                          Yes                             Yes
Repeatable read         No                          No                              Yes 
Serializable            No                          No                              No

Dirty Read Problem ->
Two transactions are running in parallel, TA and TB.
TB has updated DB status as booked, but not comitted. When transaction A reads, it reads as booked.
But if TB fails then it will rollsback, but TA has read the data as booked, this is **dirty read**

Read comitted Problem ->
If suppose Transaction A, reads same row several times and there is a chance that it reads different value
This is because the first time when it reads then status is not booked, but other transaction commits, and TA reads again now status is booked.

Phantom read problem ->
If suppose Transaction A, executes same query several times and there is a chance that the row returns are different.
Transaction A is trying to fetch a query to return row between id 1 and 5, there are only 2 rows. But after this some other transaction creates one more row with id between it, then next time TA executes it gets 3 rows.


