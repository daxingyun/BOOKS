# IPLD 模式简介
## IPLD 快速入门
	通过更多地参考 IPLD 文档的其他章节，这个“入门”部分应该能够变得更简短。
IPLD 关注分布式网络的数据层。它的范围始于数据存储和传输层之上，只对数据元素如何编码和解码为特定存储格式，然后在该编码层之上以一致且可用的形式呈现感兴趣。

IPLD 使用[数据模型](https://ipld.io/docs/data-model/)限制其标准数据元素可以采用的形式。数据模型允许在大多数编程语言中找到的标准标量数据类型和大量通用数据编码格式（JSON、CBOR 等），例如 String 和 Int。它还包括两种递归类型，用于在标量类型上构建更复杂的数据结构。这些递归类型是 List 和 Map，大多数程序员应该很熟悉，并且在许多通用数据编码格式中也很常见。IPLD 数据模型不包括某些编码格式中可用的许多类型（例如 CBOR 中可用的许多 Int 大小选项）。同样，它不支持某些编程语言中可用的许多相同类型。反而，

IPLD 的数据模型对于在数据层构建抽象非常有用。它将对编码和解码的关注推向了自己的专用领域，在这些领域中，此类关注只需要处理一组有限的数据类型以及如何与这些数据类型相互转换。但它也为图书馆和工具生态系统的发展腾出了空间，这些图书馆和工具能够建立在这个模型之上，因此可以根据关于如何呈现数据的共同假设进行操作。这样的生态系统应该能够在分布式网络社区中实现更多的算法、工具、技术和代码共享，而不是将这些资产孤立在完全与特定用例堆栈相关的代码库中。
## 建立在数据模型上
IPLD 将其数据模型视为数据表示的基础层。因此，不是将数据模型的元素称为“类型”，而是“种类”。当我们探索 IPLD 模式时，这种区别变得很重要。就数据模型的工具而言（例如编码格式），“种类”是存在于数据模型层的东西。

我们可以采用数据模型的种类列表并将它们分类为“标量种类”或“递归种类”。

- 标量种类是不包含其他种类的单一元素，例如 Int 或 String。
- 递归类型是可以包含其他类型的类型。递归类型是 Map 和 List。

IPLD 模式在不破坏数据模型的情况下引入了额外的种类，只需在现有种类上添加抽象即可。所以模式介绍：

- 联合：描述一个节点，该节点可能是许多定义明确的类型中的一种（并且只有一种）。
- 结构：通常由具有定义明确的键/值对的 map 构成。
- 枚举：特定节点必须是的一组预定义字符串或整数。

为方便起见，还引入了一个额外的 “元类型”：复制。Copy 是一种机制，Schema 作者可以借此将一个命名类型描述为复制另一个命名类型的描述符。

IPLD 模式文档使用这些种类来定义“类型”。模式“类型”指的是模式描述的数据元素，我们可以将基本类型拼凑在一起，形成更复杂的数据结构，这些数据结构具有明确定义的形状并且通常与名称相关联（对为方便起见匿名类型）。

阅读有关 [Typekinds](https://ipld.io/docs/schemas/features/typekinds/) 的更多信息。

模式是将 IPLD 的范围扩展到应用层的重要工具，在应用层中连贯和有用的数据结构很重要，而不是脱节和原子化的数据​​元素。通过这种方式，IPLD 模式提供了一个屏障，以防止数据编码和存储问题过多地泄漏到应用程序层中。相反，IPLD 可以向分布式 Web 开发人员提供清晰的数据抽象，这是一种强大的关注点分离。此外，IPLD 模式包含嵌入高级逻辑的工具，能够为双向转换提供动力，进一步将数据表示问题从应用层中排除。

## 用例
### 模式作为文档工具
在最基本的情况下，IPLD 模式只是一种描述数据属性的方法。他们这样做受 IPLD 数据模型的限制，因此没有太多的复杂性空间。IPLD 模式的一个目标是效率，这使得它们对验证很有用（见下一节），但该目标对模式 DSL 中可以表达的内容的简单性提供了额外的限制。

根据设计，IPLD 模式无法表达有关数据的各种约束。例如：

- 没有[依赖类型](https://en.wikipedia.org/wiki/Dependent_type)，因此您无法表达值之间的约束关系。
- 数据模型不表达在特定编程语言中可能有用的某些限制（例如无符号整数）。

但这些限制意味着 IPLD Schema DSL 是一种有用的文档工具，因为它很容易理解，无需事先接触太多。这与许多其他模式语言形成对比，这些模式语言试图涵盖更广泛的范围并因此遭受复杂性后果。

IPLD 模式根据 IPLD 数据模型定义基本数据布局和属性，为了文档和创作规范的目的，这提供了一个优秀的基础层。额外的层可能会在适当的时候引入约束和数据布局与特定代码的关系。IPLD 模式的未来迭代可能会引入额外的方法来表达约束，主要是为了代码生成的目的，但这些将被表达为附件而不是核心模式语言。

### 模式作为验证工具
IPLD 模式旨在高效并具有简单且可预测的路径来匹配数据布局以进行验证。IPLD 模式描述的数据布局并不详尽，但涵盖了可快速验证的最常见形式。因此，不需要深入遍历 IPLD 模式类型来提供验证反馈。

IPLD 模式中的“联合”类型提供了这种快速验证的最有趣示例。IPLD 模式仅允许您表达 “可能是 X 或 Y” 的类型，该类型可通过查看键或直接子节点的种类来验证。如果“X”和“Y”不能通过关联的密钥或它们的表示类型来区分，则它们无法被有效地验证。这些形式被认为是反模式，并且由于无法使用 IPLD 模式来表达它们而被劝阻。在大多数情况下，诸如此类的结构不佳的构造仅需要少量修改即可提供快速验证（例如，通过提供允许立即区分的鉴别器键）。

当您探索可描述和不可描述的数据布局时，IPLD 模式的这种快速验证特性将变得更加清晰。
### 模式作为版本控制和迁移工具
IPLD 模式的快速验证特性也使其成为出色的数据版本控制工具。随着序列化数据的形式随时间变化，可以使用不同的模式来表达这些形式。能够尝试针对不同模式进行验证并具有效率保证意味着 IPLD 模式可以用作数据版本控制工具。通过将一些应用于数据布局，IPLD 模式可以提供一种面向未来的机制来匹配历史形式并确定如何解释它们。

更进一步，IPLD Schemas 作为双向（解码和编码）数据描述工具，为程序员抽象表示层。将数据从旧格式迁移到新格式可以通过关注应用于模式表示数据节点的更高级别的转换功能来执行。

阅读有关[迁移和版本控制](https://ipld.io/docs/schemas/using/migrations/)的更多信息。

### 作为转换工具的模式
IPLD 模式不提供一套复杂的数据转换工具，但它们确实提供了一个基本的抽象层，可以将简单的 IPLD 数据模型类型转换为更适合应用程序设计的形式。这方面的例子包括：

- 将数据模型层的 List 或 Map 数据结构 map 到具有定义明确且成员有限的结构。
- 将数据模型层的 “可能是 X 或可能是 Y” 联合数据结构 map 到具有可预测行为和形状的具体嵌套数据结构。
- 将表示数据模型层的键/值对的元组列表 map 到 map。
- 通过转换逻辑抽象存储的数据以通过“高级布局”呈现全新的形式，其中代码与双向转换的模式相关联（在高级布局部分中有更多相关信息）。

### 模式作为代码生成工具
IPLD 模式提供了一种将序列化和反序列化过程与应用程序层数据结构连接起来的方法。因此，它们可用于生成 API 和代码，以简化和更紧密地绑定分布式 Web 应用程序的数据层。IPLD 模式作为代码生成工具的目的是简化数据管理过程，并创建比当今分布式 Web 应用程序中更清晰、更严格的抽象。

代码生成工作正在进行中。

## 模式语言：DSL 和 DMT 形式
IPLD 模式采用两种形式：专用 DSL 和通常以 JSON 形式呈现的具体化形式。DSL 旨在作为面向用户的工具的可表达性和清晰性。它可用作说明符和文档工具。DSL 还允许内联注释，并允许在换行符和空格方面有一定的灵活性。然而，具体化的形式更稳定。它不捕获注释，并且更严格地限制在 JSON 格式中。它旨在面向用户的 IPLD 模式实例将呈现 DSL，而内部编程用途将使用具体形式。[JavaScript](https://github.com/ipld/js-ipld-schema) 和 [Go](https://github.com/ipld/go-ipld-schema) 中的 IPLD Schema 工具可以在这些格式之间执行各种转换和验证。

IPLD 模式自己的内部表示也在模式语言本身中定义。这被称为“ `模式-模式` ”。DSL [形式](https://ipld.io/specs/schemas/schema-schema.ipldsch)和[数据模型树形式（作为 json）](https://ipld.io/specs/schemas/schema-schema.ipldsch.json) schema-schema 与 IPLD Schema 规范保持同步。这种模式-模式使 IPLD 模式具有自描述性，因为可以根据模式-模式验证 IPLD 模式的实例以确定它是否具有有效形式。IPLD Schema 形式有一些额外的约束，这些约束没有严格包含在 schema-schema 本身中，例如围绕类型名称的有效字符的规则。虽然 schema-schema 中的注释使其成为理解 IPLD 模式的内部表示的非常有用的文档，但需要额外的规范，特别是对于 schema-schema 未充分涵盖的 DSL。

# 比较
## IPLD 模式与其他模式语言
- 结构类型

	IPLD 模式基于结构类型（与主格类型不同）。
	
	这意味着模式信息并未嵌入数据本身。因此，即使数据是在没有模式的情况下生成的，IPLD 模式也可以描述数据。并且可以使用不同的模式以不同的方式验证和查看相同的数据！
- 没有直接耦合到 links 格式
- 对串行转换的精细控制

## 模式与 ADL
IPLD 模式被设计为计算上可预测的。它们比 ADL 更受限制。（ADL 具有类似“插件”的结构：它们的复杂性没有真正的限制。）

因此，即使在受限计算环境或可预测性很重要的其他场景中，IPLD 模式也可以相对安全地使用。相比之下，对于 ADL，实现需要审计——并且每个 ADL 都需要自己的审计。

模式是双向的。您可以将模式视为数据的“镜头”。ADL 有时是双向的，但这是实现者的心血来潮。

# 目标
- 提供合理、易于使用的通用类型系统，用于声明有关数据的有用属性。
- 在 IPLD [数据模型](https://ipld.io/docs/data-model/) 上很好地组合：架构应该可用于您可以为其构建 IPLD [编解码器](https://ipld.io/docs/codecs/)的任何数据格式。
- 高效验证：可预测；数据和模式的大小大致呈线性关系；而且绝对没有图灵完整。
- 与语言无关：模式工具的许多兼容实现应该存在，以及许多语言的绑定。
- 协助而不是阻碍迁移：我们希望使用现有数据；我们需要好好处理这个案子。
- 成为在协作和文档中增加价值的工具：模式应该为 API 文档提供一个自然的位置，并且是一个合理的设计文献。

总而言之：使去中心化和分布式应用程序的开发更容易、更清晰、更健壮。

# 架构功能摘要
## 描述通用数据形式的结构
IPLD 模式介绍了在许多编程生态系统中都广为人知的基础知识（求和类型、乘积类型、一些特定的递归类型）：

- map

		{Foo:Bar}
- list

		[Foo]
- primitives

		type Foo int
- Structs

		type FooBar struct {
		  f Foo
		  b Bar
		}
- 可区分的联合（几种与野外常见的样式相匹配的样式）

		type union FooOrBar {
		  Foo "f"
		  Bar "b"
		} representation keyed
- Enumerations

		type FBB enum {
		  | "Foo"
		  | "Bar"
		  | "Baz"
		}
- “可能”数据元素的简单语法

		type Foo struct {
		  f nullable Bar
		}

		type Bar [nullable Foo]
- 非必填字段的清晰语法

		type Foo struct {
		  f optional Bar
		}
- 用于使用编程逻辑透明地转换数据的挂钩

		advanced ROT13
		type EncryptedString string representation advanced ROT13

## map 到数据模型
所有这些都 map 到 IPLD 数据模型：

- 每种类型都有一个表示。例如 Maps 表示为 Maps，Structs 也表示为 Maps。
- 表示可以为序列化的字段名称指定一个 map，这在诸如需要序列化紧凑性但为了描述目的而更喜欢模式中的冗长性等情况下很有用。
- 表示是可定制的，包括将一种类型完全 map 到不同的表示类型。例如，可以将 Struct 声明为具有 List 表示（如果不那么自描述，则使其更短以进行序列化）；或者 Struct 可以用简单的字符串模式表示。

您可能想了解一些其他 IPLD 功能，这些功能可以比模式更进一步：“高级数据布局 (ADL) ” 定义可以充当已经熟悉的数据类型，例如 map 或列表或字节（字节数组），同时使用完全可插拔的系统将内容转换为其他形式进行表示。此类功能的常见用途是将数据拆分为完全独立的块进行存储，从而允许：

- 非常大的字节数组存储在许多不同的块中，呈现为单个可迭代的字节类型。
- 以 Map 或 List 类型呈现的大型数据集的分片抽象。
- 静态加密的透明连接呈现为加密数据的未加密形式。

...但是，有关这些的更多详细信息，[请参阅 ADL 的文档章节](https://ipld.io/docs/advanced-data-layouts/)。ADL 与架构一起工作得很好，但被认为是 IPLD 堆栈的不同部分。

所有适用于 IPLD 数据模型的工具也适用于模式：

- 遍历
- 路径
- 选择器
- ETC

所有通用 IPLD 算法都可以在模式节点上工作，其方式与在普通数据模型中的节点上工作的方式完全相同。这允许新的行为，例如通过字段名称遍历 Struct，即使 Struct 表示是一个列表。