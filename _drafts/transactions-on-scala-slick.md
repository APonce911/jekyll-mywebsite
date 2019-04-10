---
title: "SSO Introduction"
date: 2019-03-25 10:41:00
<!-- lang: en -->
ref: transactions-on-scala-slick

---

<h2>What is a Transaction?</h2>

<h2>Why is it good?</h2>
BecauseWithout it all db actions are in auto-commit.
<h2>When it should be used?</h2>

<h2>How it can be implemented?</h2>

1. scala.dbc.statement package
   class Transaction
   https://www.scala-lang.org/api/2.6.0/scala/dbc/statement/Transaction.html

2. create own Transaction class
   find some open source repo with an example
   https://stackoverflow.com/questions/41219200/how-to-use-transaction-in-slick

3. Reflection
   what is it?

<h2>What are the alternatives?</h2>
1. Futures

<!-- ------------------------------------------------ -->
http://slick.lightbend.com/doc/3.2.0/dbio.html
http://slick.lightbend.com/doc/3.2.0/api/index.html#slick.dbio.DBIOAction
https://docs.scala-lang.org/overviews/core/futures.html

Anything that you can execute on a database is an instance of a DBIO Action

You can use the <i>run</i> method to execute a DBIOAction on a Database and produce a materialized result.

Execution of the action starts in the background when run is called. The materialized result is returned as a Future which is completed asynchronously as soon as the result is available.

Example:

<pre>
 <code>
  val q = for (c <- coffees) yield c.name
  val a = q.result
  val f: Future[Seq[String]] = db.run(a)

  f.onSuccess { case s => println(s"Result: $s") }
 </code></pre>

Composing DBIO Actions

DBIOActions describe individual actions to execute in a sequential order on one database session.
They eventually result in <i>Success</i> or <i>Failure</i>

Sequential Execution

Unless specifically noted, all combinators only apply to successful actions. Any failure will abort the sequence of execution and result in a failed Future or Reactive Stream.

Use <i>DBIO.seq</i> and <i>DBIO.sequence</i> to create a sequential execution.

Transactions and Pinned Sessions

Use <i>withPinnedSession</i> to force the use/start of a session, even when not waiting for a non-DB response.

<i>transactionally</i> is used to force a transaction, this guarantees that the entire DBIOAction that is executed will either succeed or fail automatically. Without it and db actions are in auto-commit. This implies a pinned session.

<pre>
 <code>
  val a = (for {
    ns <- coffees.filter(_.name.startsWith("ESPRESSO")).map(_.name).result
    _ <- DBIO.seq(ns.map(n => coffees.filter(_.name === n).delete): _*)
  } yield ()).transactionally

  val f: Future[Unit] = db.run(a)
 </code></pre>
