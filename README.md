StarlingMVC Framework
===========

����ע
-----------
������[Luke Cheng](mailto:chengogng8@gmail.com)���룬��ӦStarlingMVCԭ�棬�������ԭgithub: https://github.com/CreativeBottle/starlingMVC��
��û�а���ԭ���ϸ��룬�ڷ�������У���������һЩ�Լ���ע�͡��������������Ļ��������Ķ�ԭ�ġ�

StarlingMVC Framework===========
StaringMVC��һ��ʹ��[Starling](http://gamua.com/starling/)��������ϷIOC��ܣ�����[Swiz](http://swizframework.org/)��[RobotLegs](http://www.robotlegs.org/)���ơ����������ԣ�

* ����ע��(DI)/���Ʒ�ת(IOC)
* ��ͼ�ٲ�(View Mediation)* �¼�����
* ��Ӱ��ԭ����Starling��Ϸ����
* ��������
* ����չ
* �ṩһЩʵ�ù���

StarlingMVC���ʹ��[Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)��Դ��Ȩ

��������
------------
* [Flex SDK 4.6](http://www.adobe.com/devnet/flex/flex-sdk-download.html)
* [Starling 1.1](http://gamua.com/starling/)
* [FlexUnit 4.1 (For running the unit tests)](http://www.flexunit.org/)

������
------------
* [Creative Bottle, Inc](http://www.creativebottle.com)
* [Scott Jeppesen](mailto:scott.jeppesen@creativebottle.com)
* [Tom McAvoy](mailto:tom.mcavoy@creativebottle.com)

��������
------------ֻ��Ҫ�򵥵ļ��оͿ��Լ���Starling������Ҫʵ����StringMVC�ࣨ���ǻ�����Starling��ʾ�ࣩ���ṩ��������starling��ʾ�ĸ�����StarlingMVCConfig����ʵ��������һЩ����Ϸ����Ҫʹ�õ�bean��

```as3
package com.mygame.views
{
  	import com.creativebottle.starlingmvc.StarlingMVC;
	import com.creativebottle.starlingmvc.config.StarlingMVCConfig;
	import com.creativebottle.starlingmvc.views.ViewManager;
 	import com.mygame.models.GameModel;

	import starling.core.Starling;
	import starling.display.Sprite;

	public class GameMain extends Sprite
	{
		private var starlingMVC:StarlingMVC;

		public function GameMain()
		{
			var config:StarlingMVCConfig = new StarlingMVCConfig();
			config.eventPackages = ["com.mygame.events"];
			config.viewPackages = ["com.mygame.views"];

			var beans:Array = [new GameModel(), new ViewManager(this)];

			starlingMVC = new StarlingMVC(this, config, beans);
		}
	}
}
```

���ϴ��룬StarlingMVCConfig��������StarlingMVC������Ҫ�����event��view�ֱ�����Щ���
bean���������һ�Ѷ���Ҳ�����ǵ��������ǿ������������͡�

###Flash Builder��Ҫ�������õĻ���
When exporting release builds using Flash Builder, the ActionScript compiler will strip out non-standard metadata unless it is instructed otherwise. StarlingMVC's custom metadata is required in order for powerful features such as automatic dependency injection (DI) to work correctly and so the removal of the metadata can effectively render your application useless.

����Flash builder�����ʱ��ActionScript������������δ�����Ĺؼ��֡�StarlingMVC��Ҫ���ƻ������ؼ�����ʵ��һЩ�Ƚ�ǿ������ԣ�������ע�롣��������Ҫ��������һ�¹ؼ��֡�

�����ؼ��ֵķ���������Ĺ��������ñ���ѡ�

�Ҽ��������-����-ActionScript���룬�ڸ��ӱ�������������������ݣ�
```
-keep-as3-metadata+=Dispatcher
-keep-as3-metadata+=EventHandler
-keep-as3-metadata+=Inject
-keep-as3-metadata+=Juggler
-keep-as3-metadata+=PostConstruct
-keep-as3-metadata+=ViewAdded
-keep-as3-metadata+=ViewRemoved
```

Beans
------------
Bean������ҪStarlingMVC�йܵĶ���Bean����ע�롢��ע�롢�����¼��������¼��ֳ�ʼ��Bean�ķ�ʽ��

###ֱ��ʵ��������
```as3
var beans:Array = [new GameModel(), new ViewManager(this)];
```


###ʵ����Bean
```as3
var beans:Array = [new Bean(new GameModel()), new Bean(new ViewManager(this))];
```

�ṩBeanʵ���ķ�ʽ������������ƣ��������ַ�ʽ��������ָ��һ��id�������������������ע���ʱ��ʹ�����id�ˡ����⣬bean��starlingMVC���ǰ��ౣ��ģ������������bean��ͬ�����࣬�������id�������ǡ����磺

```as3
var beans:Array = [new Bean(new GameModel(),"gameModelEasy"),new Bean(new GameModel(),"gameModelHard"), new ViewManager(this)];
```

###ʹ��BeanProvider
BeanProvider�ṩbean�ļ��ϣ�provider����һ��beans�����飬����װ���κ��������ݣ����������ٰ�����һ��BeanProvider

```as3
package com.mygame.config
{
	import com.creativebottle.starlingmvc.beans.BeanProvider;
	import com.mygame.assets.AssetModel;
	import com.mygame.models.AudioModel;
	import com.mygame.models.GameModel;

	public class Models extends BeanProvider
	{
		public function Models()
		{
			beans = [new GameModel(), new Bean(new AudioModel(),"audioModel"), new AssetModel()];
		}
	}
}
```
����ʹ��BeanProvider��������ȽϺ���֯�Լ��Ĵ��롣

```as3
var beans:Array = [new Models(), new ViewManager(this)];
```

###ProtoBeans
ProtoBean����һ�ַ�ʽ������ע���ʱ��ʵ��������������bean���ṩһ��������������Ҫ�ṩ�������ͺ�id��

```as3
var beans:Array = [new ProtoBean(Character,"character"), new ViewManager(this)];
```
ʹ��ProtoBean��StarlingMVC������������ʵ������ÿ������ע���ʱ�򣬶�������һ���µ�ʵ��������������У�"Character"�಻��������ͨbeanһ��ʹ�õ���ģʽ���������Լ�ֱ���ڴ�����"new Character()"����ʽ�����ַ�ʽ���ŵ���StarlingMVC���԰������Charcter�ڲ�������ע�롣

����ע�루Dependency Injection��
------------
���������е�bean�ϻ�Starling����ʾ����display objects����ʹ������ע�롣����ע��ķ�ʽ����public���Ի�getter/setter��ʹ��"Inject"ע�⡣�磺
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject]
		public var gameModel:GameModel;

		public function GameController():void
		{

		}
	}
}
```
����ʹ��id��
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject(source="gameModel")]
		public var gameModel:GameModel;

		public function GameController():void
		{

		}
	}
}
```
������������У����GameModel��һ��bean��StarlingMVC���ڿ�ܳ�ʼ����ʱ�򣬽����ĵ���ʵ�����������һ��protobean�������ע���ʱ��ʵ������

Starling��֧��ע��bean�еı��������ַ�ʽҪ��bean���빹���ʱ��ָ��id(�� `new Bean(new GameModel(),"gameModel");`)��ע��bean�еı�����ôд��

```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject(source="gameModel")]
		public var gameModel:GameModel;

		[Inject(source="userModel.currentUser")]
		public var currentUser:User;

		public function GameController():void
		{

		}
	}
}
```

������������У�`userModel`��`currentUser`�ᱻע�뵽���controller�С�StarlingMVC֧�ֶ��ε�����ע�룬�����㻹������ô�ã�`[Inject(source="userModel.currentUser.firstName")]`

###��(Binding)

StarlingMVC��֧�ְ�ģʽ��������ÿ�θ��µ�ʱ�򽫻��Զ�ˢ��ע�롣

```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject(source="gameModel")]
		public var gameModel:GameModel;

		[Inject(source="userModel.currentUser", bind="true")]
		public var currentUser:User;

		public function GameController():void
		{

		}
	}
}
```
����Injectע���е� bind="true"�����а󶨣���userModel��currentUser���µ�ʱ��StarlingMVC���Զ��Ķ԰󶨵�ע����и��¡�ͬʱ��Ҳ���԰󶨵�getter/setter�����������Ϳ��Ժ����ŵĴ������Եĸı��������Ϸ�е�չʾ/�߼��仯��

```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject(source="gameModel")]
		public var gameModel:GameModel;

		[Inject(source="userModel.currentUser", bind="true")]
		public function set currentUser(value:User):void
		{
			_currentUser = value;

			// Do something to update your UI with the new value
		}

		public function get currentUser():User
		{
			return _currentUser;
		}
		private var _currentUser:User;

		public function GameController():void
		{

		}
	}
}
```
Binding is connected directly to the Starling juggler instance and will check for changes on each bound property everytime the `advanceTime()` method is called. This does not provide a binding that works as instantaneously as Flex binding. Binding should be used sparingly as there is still overhead to check for changes to the bound properties.

As an alternative to auto bound properties, StarlingMVC supports binding through invalidation. This method is much more efficient than the auto bound properties because it give you much more control over when properties are updated. This is done through an injected `Bindings` class and the optional "auto" parameter.
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject(source="gameModel")]
		public var gameModel:GameModel;

		[Inject(source="userModel.currentUser", bind="true", auto="false")]
		public function set currentUser(value:User):void
		{
			_currentUser = value;

			// Do something to update your UI with the new value
		}

		public function get currentUser():User
		{
			return _currentUser;
		}
		private var _currentUser:User;

		public function GameController():void
		{

		}
	}
}

package com.mygame.models
{
	public class UserModel
	{
		[Bindings]
		public var bindings:Bindings;

		public function set currentUser(value:User):void
		{
			if(value != _currentUser)
			{
				_currentUser = value;

				bindings.invalidate(this, "currentUser");
			}
		}

		public function get currentUser():User
		{
			return _currentUser;
		}
		private var _currentUser:User;
	}
}
```

Events
------------
###Dispatching Events
Events in StarlingMVC are dispatched in one of two ways:
1) StarlingMVC contains a global instance of `starling.events.EventDispatcher`. The quickest way to dispatch an event into the StarlingMVC framework is to use this dispatcher. This dispatcher can be injected into your bean by using the `[Dispatcher]` metadata tag.
2) DisplayObjects can dispatchEvents using their own `dispatchEvent()` method. This is only available to DisplayObjects and the events must set `bubbles=true'.

###Handling Events
Event handlers are denoted by using the `[EventHandler(event="")]` metadata tag on a public method of a bean. The event argument in the tag can contain one of two options: the event type string
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[EventHandler(event="scoreChanged")]
		public function scoreChanged(event:ScoreEvent):void
		{

		}
	}
}
```
or the typed event
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[EventHandler(event="ScoreEvent.SCORE_CHANGED")]
		public function scoreChanged(event:ScoreEvent):void
		{

		}
	}
}
```
By using the second approach, you will gain the benefit that StarlingMVC will type check any of the events during initialization and throw and error if the event or event type doesn't exist. This protects against typos.

In both examples above, the handler must accept the type of the dispatched event to handle. However, a second optional parameter exists in the EventHandler tag that will allow you to specify specific properties of the event to use as parameters to the event handler. For example:
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[EventHandler(event="ScoreEvent.SCORE_CHANGED", properties="user, newScore")]
		public function scoreChanged(user:User, newScore:int):void
		{

		}
	}
}
```
In the above example, instead of passing the entire event into the handler, StarlingMVC will pass only the "user" and "newScore" properties. Note that the types must match or an error will be thrown.

View Mediation
------------
View mediators are a great way of keeping your view classes separate from the code that controls them. A view mediator is set up just like any other bean. To link a view to a view mediator a `[ViewAdded]` metadata tag is used on a public method. When a DisplayObject is added to the stack, StarlingMVC will look for instances of the ViewAdded tag. If the parameter of any ViewAdded methods are of the type of the view that was just added, the new DisplayObject will be passed to that method. To unlink a mediator from a view when the view has been removed the `[ViewRemoved]` metadata tag is used.
```as3
package com.mygame.mediators
{
	public class GameMediator
	{
		private var view:Game;

		[ViewAdded]
		public function viewAdded(view:Game):void
		{
			this.view = view;
		}

		[ViewRemoved]
		public function viewRemoved(view:Game):void
		{
			this.view = null;
		}
	}
}
```
Bean Lifecycle
------------
Normal beans are set up on initialization. However, since the dependency injection and event handling happens after creation bean values are not available immediately. To receive notification of when a bean has been fully processed we can add the `[PostConstruct]` tag to a public method. This method will be automatically called when all DI has been completed. Similarly, when a bean is being destroyed we can specify a public method to be called with the `[PreDestroy]` tag. This works in all standard beans and DisplayObjects.
```as3
package com.mygame.controllers
{
	public class GameController
	{
		[Inject]
		public var gameModel:GameModel;

		[PostConstruct]
		public function postConstruct():void
		{
			// set up code here
		}

		[PreDestroy]
		public function preDestroy():void
		{
			// tear down code here
		}

		[EventHandler(event="ScoreEvent.SCORE_CHANGED", properties="user, newScore")]
		public function scoreChanged(user:User, newScore:int):void
		{

		}
	}
}

package com.mygame.controllers
{
	public class GameModel
	{
		[Bindings]
		public var bindings:Bindings;

		public function set score(value:int):void
		{
			if(value != _score)
			{
				_score = value;

				bindings.invalidate(this, "score");
			}
		}

		public function get score():int
		{
			return _score;
		}
		private var _score:int;
	}
}
```
In the above example you can see that in the controller the Inject tag includes "auto='false'". This disables the auto binding so that a check is not done on every iteration of the Juggler. In the GameMode, we are injecting the Bindings instance and then invalidating manually when the property changes. Once the property is invalidated, it will be automatically updated on the next pass of the juggler.

Manual Bean Creation/Removal
------------
Manual bean creation and removal is done through the event system. Dispatching `BeanEvent.ADD_BEAN` will add and process a new bean. Dispatching `BeanEvent.REMOVE_BEAN` will remove the bean from the system.
```as3
package com.mygame.view
{
	public class Game
	{
		public var gamePresentationModel:GamePresentationModel;

		[PostConstruct]
		public function postConstruct():void
		{
			gamePresentationModel = new GamePresentationModel();

			dispatchEvent(new BeanEvent(BeanEvent.ADD_BEAN, gamePresentationModel));
		}

		[PreDestroy]
		public function preDestroy():void
		{
			dispatchEvent(new BeanEvent(BeanEvent.REMOVE_BEAN, gamePresentationModel));

			gamePresentationModel = null;
		}
	}
}
```
In the example above, we create a presentation model for our view and add it to StarlingMVC as a bean. In doing this, the PM will be processed as a bean and gain all of the benefits of DI and EventHandling.

Command Pattern
------------
StarlingMVC includes support for the command pattern. Commands are essentially beans that are created when a specified event is dispatched, executed, and then disposed of. To add a command to the framework, an instance of the Command class should be added to the beans.
```as3
package com.mygame.views
{
  	import com.creativebottle.starlingmvc.StarlingMVC;
	import com.creativebottle.starlingmvc.config.StarlingMVCConfig;
	import com.creativebottle.starlingmvc.views.ViewManager;
 	import com.mygame.models.GameModel;

	import starling.core.Starling;
	import starling.display.Sprite;

	public class GameMain extends Sprite
	{
		private var starlingMVC:StarlingMVC;

		public function GameMain()
		{
			var config:StarlingMVCConfig = new StarlingMVCConfig();
			config.eventPackages = ["com.mygame.events"];
			config.viewPackages = ["com.mygame.views"];

			var beans:Array = [new GameModel(), new ViewManager(this), new Command(DoSomethingEvent.DO_SOMETHING, DoSomethingCommand)];

			starlingMVC = new StarlingMVC(this, config, beans);
		}
	}
}
```
This will map the event to the command. The command class can receive all of the same injections as any other bean. It cannot handle events, however, since the instance will only exist long enough to execute a single command. The method to execute in the command instance is noted with the `[Execute]` metadata.
```as3
package com.mygame.commands
{
	import com.mygame.events.NavigationEvent;
	import com.mygame.models.BubbleModel;

	import starling.events.EventDispatcher;

	public class DoSomethingCommand
	{
		[Dispatcher]
		public var dispatcher:EventDispatcher;

		[Inject]
		public var bubbleModel:BubbleModel;

		[Execute]
		public function execute(event:DoSomethingEvent):void
		{
			trace("did something!");
		}
	}
}
```
In this example, whenever the `DoSomethingEvent.DO_SOMETHING` is dispatched, StarlingMVC will create an instance of DoSomethingCommand, run the execute method, and then dispose of the instance. The Command class also contains an optional parameter called runOnce.
```as3
package com.mygame.views
{
  	import com.creativebottle.starlingmvc.StarlingMVC;
	import com.creativebottle.starlingmvc.config.StarlingMVCConfig;
	import com.creativebottle.starlingmvc.views.ViewManager;
 	import com.mygame.models.GameModel;

	import starling.core.Starling;
	import starling.display.Sprite;

	public class GameMain extends Sprite
	{
		private var starlingMVC:StarlingMVC;

		public function GameMain()
		{
			var config:StarlingMVCConfig = new StarlingMVCConfig();
			config.eventPackages = ["com.mygame.events"];
			config.viewPackages = ["com.mygame.views"];

			var beans:Array = [new GameModel(), new ViewManager(this), new Command(DoSomethingEvent.DO_SOMETHING, DoSomethingCommand, true)];

			starlingMVC = new StarlingMVC(this, config, beans);
		}
	}
}
```
In this example, the command bean is added with the following line: `new Command(DoSomethingEvent.DO_SOMETHING, DoSomethingCommand, true)`. The optional last parameter, `true`, specifies that this command should be run once. So in this case, when the DO_SOMETHING event is dispatched, the framework would create an instance of DoSomethingCommand, run execute, dispose of the instance, and then remove the mapping. This functionality is very useful for initialization commands.

EventMap
------------
EventMap is a utility class for creating and managing event listeners. Using EventMap exclusively to create listeners within your class makes cleanup very easy.
```as3
package com.mygame.mediators
{
	import com.creativebottle.starlingmvc.events.EventMap;

	public class GameMediator
	{
		private var eventMap:EventMap = new EventMap();

		[ViewAdded]
		public function viewAdded(view:Game):void
		{
			eventMap.addMap(view.playButton,TouchEvent.TOUCH, playButtonTouched);
			eventMap.addMap(view.instructionsButton,TouchEvent.TOUCH, instructionsTouched);
		}

		[ViewRemoved]
		public function viewRemoved(view:Game):void
		{
			event.removeAllMappedEvents();
		}

		private function playButtonTouched(event:TouchEvent):void
		{

		}

		private function instructionsButtonTouched(event:TouchEvent):void
		{

		}
	}
}
```
Juggler
------------
The Juggler class in Starling is used to handle all animation within a game. For a class to take advantage of the Juggler instance, it must implement the IAnimatable interface but defining `advanceTime(time:Number)`. The global juggler reference can be accessed as a static property of Starling as `Starling.juggler1`. However, this property can also be directly injected into your class instances using the `[Juggler]` tag.
 ```as3
 package com.mygame.mediators
 {
 	import com.creativebottle.starlingmvc.events.EventMap;

 	public class GameMediator implements IAnimatable
 	{
 		[Juggler]
        public var juggler:Juggler;

 		[ViewAdded]
 		public function viewAdded(view:Game):void
 		{
 			juggler.add(this);
 		}

 		[ViewRemoved]
 		public function viewRemoved(view:Game):void
 		{
 		    juggler.remove(this);
 		}

 		public function advanceTime(time:Number):void
 		{
            // do some animation logic
 		}
 	}
 }
 ```

ViewManager
------------
ViewManager is a utility class to facilitate creating views and adding/removing them from the stage. When creating the instance of ViewManager the constructor requires a reference to the root view of the game (i.e. `new ViewManager(this)`) from the root DisplayObject. Adding the ViewManager instance to the StarlingMVC beans makes it easy to swap views from anywhere in the Starling application.
###setView
Calls to setView will remove existing views and add the new view. ViewManager handles instantiating the view and adding it to the stack.
```as3
package com.mygame.controllers
{
	public class NavigationController
	{
		[Inject]
		public var viewManager:ViewManager;

		[EventHandler(event="NavigationEvent.NAVIGATE_TO_VIEW", properties="viewClass")]
		public function navigateToView(viewClass:Class):void
		{
			viewManager.setView(viewClass);
		}
	}
}
```
###addView
Calls to addView will add a new view on top of the existing view. This is handy for popups, HUDs, etc. Whereas setView accepts a parameter of type Class, addView accepts a view instance.
```as3
package com.mygame.views
{
	public class Game
	{
		[Inject]
		public var viewManager:ViewManager;

		private var hud:GameHUD;

		[PostConstruct]
		public function postConstruct():void
		{
			hud = new GameHUD();

			viewManager.addView(hud);
		}
	}
}
```
###removeView
Calls to removeView will remove the specified view from the stack.
###removeAll
Calls to removeAll will remove all views from the stack. This is called automatically when calling `setView()`.
