---
layout: post
title: Linq中GroupBy的应用
categories: [IT, CSharp]
tags: [Linq, CSharp]
fullview: true
---

#Group
Group是进行分组操作，同SQL中的Group By类似。
接口原型：

	public static IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector);

	public static IEnumerable<TResult> GroupBy<TSource, TKey, TResult>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TKey, IEnumerable<TSource>, TResult> resultSelector);

	public static IEnumerable<IGrouping<TKey, TElement>> GroupBy<TSource, TKey, TElement>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TSource, TElement> elementSelector);

	public static IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, IEqualityComparer<TKey> comparer);

	public static IEnumerable<TResult> GroupBy<TSource, TKey, TResult>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TKey, IEnumerable<TSource>, TResult> resultSelector, IEqualityComparer<TKey> comparer);

	public static IEnumerable<TResult> GroupBy<TSource, TKey, TElement, TResult>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TSource, TElement> elementSelector, Func<TKey, IEnumerable<TElement>, TResult> resultSelector);

	public static IEnumerable<IGrouping<TKey, TElement>> GroupBy<TSource, TKey, TElement>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TSource, TElement> elementSelector, IEqualityComparer<TKey> comparer);

	public static IEnumerable<TResult> GroupBy<TSource, TKey, TElement, TResult>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TSource, TElement> elementSelector, Func<TKey, IEnumerable<TElement>, TResult> resultSelector, IEqualityComparer<TKey> comparer);

接口重载返回两种类型 IEnumerable<TResult> 和 IEnumerable<IGrouping<TKey, TElement>>
示例：


	// 1. Lambda表达式方式
	var result = from score in DataSource.Scores 
             group score by score.StudentID into scoreGroup 
             select scoreGroup;

    // 2. 链式表达式方式
    var result = ScoreList.GroupBy(s => s.StudentID, s => s);

其中scoreGroup为IGrouping<TKey, TSource>类型，返回结果为IEnumerable<IGrouping<TKey, TSource>>
IGrouping<TKey, TSource>>接口原型：

	public interface IGrouping<out TKey, out TElement> : IEnumerable<TElement>, IEnumerable
    {
        TKey Key { get; }
    }

其中Key为分组依据的字段

	foreach (var score in result)
	{
		var studentID = score.Key;
		var list = score.ToList();
	}

