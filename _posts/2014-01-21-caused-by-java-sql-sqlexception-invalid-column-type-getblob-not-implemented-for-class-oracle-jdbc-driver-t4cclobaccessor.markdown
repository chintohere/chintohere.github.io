---
author: chintohere
comments: true
date: 2014-01-21 23:47:28+00:00
layout: post
slug: caused-by-java-sql-sqlexception-invalid-column-type-getblob-not-implemented-for-class-oracle-jdbc-driver-t4cclobaccessor
title: 'Caused by: java.sql.SQLException: Invalid column type: getBLOB not implemented
  for class oracle.jdbc.driver.T4CClobAccessor'
wordpress_id: 258
---

Ever seen this. This usually happens when the db column in question is not a BLOB.

In my case, the column was a CLOB. You wouldn't think it should work, but it doesn't.


        Caused by: java.sql.SQLException: Invalid column type: getBLOB not implemented for class oracle.jdbc.driver.T4CClobAccessor
                at oracle.jdbc.driver.DatabaseError.throwSqlException(DatabaseError.java:113) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.DatabaseError.throwSqlException(DatabaseError.java:147) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.Accessor.unimpl(Accessor.java:359) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.Accessor.getBLOB(Accessor.java:1301) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.OracleResultSetImpl.getBLOB(OracleResultSetImpl.java:1281) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.OracleResultSetImpl.getBlob(OracleResultSetImpl.java:1467) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at oracle.jdbc.driver.OracleResultSet.getBlob(OracleResultSet.java:1979) ~[ojdbc14-10.2.0.5.0.jar:Oracle JDBC Driver version - "10.2.0.5.0"]
                at org.apache.commons.dbcp.DelegatingResultSet.getBlob(DelegatingResultSet.java:565) ~[commons-dbcp-1.4.jar:1.4]
                at org.apache.commons.dbcp.DelegatingResultSet.getBlob(DelegatingResultSet.java:565) ~[commons-dbcp-1.4.jar:1.4]
                at org.hibernate.type.descriptor.sql.BlobTypeDescriptor$5.doExtract(BlobTypeDescriptor.java:115) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.type.descriptor.sql.BasicExtractor.extract(BasicExtractor.java:64) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.type.AbstractStandardBasicType.nullSafeGet(AbstractStandardBasicType.java:254) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.type.AbstractStandardBasicType.nullSafeGet(AbstractStandardBasicType.java:250) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.type.AbstractStandardBasicType.nullSafeGet(AbstractStandardBasicType.java:230) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.type.AbstractStandardBasicType.hydrate(AbstractStandardBasicType.java:331) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.persister.entity.AbstractEntityPersister.hydrate(AbstractEntityPersister.java:2283) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.loadFromResultSet(Loader.java:1527) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.instanceNotYetLoaded(Loader.java:1455) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.getRow(Loader.java:1355) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.getRowFromResultSet(Loader.java:611) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.doQuery(Loader.java:829) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.doQueryAndInitializeNonLazyCollections(Loader.java:274) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                at org.hibernate.loader.Loader.loadEntity(Loader.java:2037) ~[hibernate-core-3.6.10.Final.jar:3.6.10.Final]
                ... 17 common frames omitted
        `


