---
layout: post
title:  "Abstract Factory Pattern"
date:   2021-05-29 23:32:04 +0700
categories: [bash, linux, ubuntu]
---

# Abstract Factory Pattern

생성일: 2021년 5월 29일 오후 12:48

1. 추상 팩토리 패턴이란?

  다양한 구성 요소 별로 객체의 집합을 생성해야 할때 유용한 패턴. 

클라이언트가 추상 팩토리와 추상데이터에 의존하게 하여, 특정한 인터페이스를 갖춘 객체가 아닌 상황에 따라 다양한 객체를 생성하고 참조할 수 있게 함. 

2. UML

![Abstract%20Factory%20Pattern%20c578491863b147528ca74c14f230e95c/Untitled.png](Abstract%20Factory%20Pattern%20c578491863b147528ca74c14f230e95c/Untitled.png)

3. Code

```kotlin
enum class GraphEnum {
    CIRCLE, BAR
}

interface IGraph {
	fun draw()
}

interface IGraphFactory{
	fun createGraph() : IGraph 
}

class CircleGraph : IGraph {
	override fun draw() = println("원형 그래프")
	
}

class BarGraph : IGraph {
	override fun draw() = println("막대 그래프")
}

class BarGraphFactory : IGraphFactory {
	override fun createGraph() : IGraph = BarGraph()
}

class CircleGraphFactory : IGraphFactory {
	override fun createGraph() : IGraph = CircleGraph()
}

class GraphProgram(private val graph : GraphEnum){
	fun run() {
		val factory : IGraphFactory = when(graph) {
			GraphEnum.CIRCLE -> {
				CircleGraphFactory()
			}
			GraphEnum.BAR -> {
				BarGraphFactory()
			}
		}
		
		factory.createGraph().run { draw() }
	}
}

```