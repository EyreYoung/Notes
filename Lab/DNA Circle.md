# DNA Circle

## DNA Circle White Paper

### 2. Motivation

#### 目标

1. 组织成员的IBD匹配

2. 为个人的家谱研究提供支持证据

3. 连接遥远的家谱亲戚



<img src="img/DNA2.1.png" alt="Attachment.png" style="zoom: 50%;" />

#### 2.1. IBD匹配

对祖先DNA的IBD分析可确定在成对祖先DNA成员之间共享的IBD的基因组片段，并使用IBD的数量来估计个体之间的关联程度。

鉴于此IBD分析是在所有成对的AncestryDNA成员中进行的，一个成员可能有成百上千的已识别远亲。

尽管一个人可能与成千上万的其他活着的个体按相同的血统共享DNA，但祖先的数量有限，可以通过这些祖先来继承。

一个人的祖先的数量（在合理的世代数量之内）通常比那个人的同居亲戚的数量少得多。



因此，在已知共同祖先的情况下，可以由可能对IBD负责的祖先对许多IBD识别的亲属进行分组。

这是DNA Circles的首要目标。 

IBD匹配的这种分组允许用户通过与特定组中每个亲戚的协作来对每个祖先执行定向研究。



为了说明这一点，请考虑图2.1，它是四个祖先的基因组遗传遗传的图形表示。

每个基因组均表示为基因组序列或单倍型的连续块。

在祖先中重组后，第2代的孩子继承了原始祖先基因组的块。四到六代后，原始祖先基因组的那些块出现在一组三个后代中。



如果两个人从同一个祖先那里继承了相同的DNA片段，那么该DNA被称为“后代相同”或IBD。 在该示例中，个人D与个人C和E共享DNA IBD。假设有家谱信息，则可以通过追溯其血统来识别任何两个人的共同祖先。 遇到的第一个共同祖先称为***最新的共同祖先***，即***MRCA***。 在回溯C，D和E的血统书时，祖先A将被识别为D的MRCA与C，以及D的MRCA与E。



通过将D与C和E分组到一个DNA圈中，D可以将这两个个体（C和E）与他共享DNA的其他数千个个体区分开来-并通过祖先A将其归类为与他有亲戚关系。

#### 2.2. 家谱研究的支持证据

第二，祖先DNA成员的血统通常是详细家谱研究的结果，该研究涉及整合各种历史文献中的信息以支持或识别祖传世系。 通过将整个AncestryDNA成员数据库中的IBD和家谱信息结合在一起，除历史记录外，DNA Circles还可被视为成员家谱的另一种支持证据。



图2.1也说明了这一概念。 将祖先A识别为个人C和D之间的MRCA，有证据支持C和D可能都继承了该祖先的DNA。 然后，我们添加了一个知识，即个体E也具有与个体D的IBD片段（除了共享祖先A作为其MRCA）。 这为祖先A提供了另外的证据，作为个人D的血统书的一部分，因此也为C和E的遗物提供了证据。



因此，一组个体（此处为包括个体C，D和E的DNA圈；图2.1）之间的两个独立信息（谱系关系和IBD共享模式）之间的一致性可以作为已证明谱系的支持证据 线。 我们注意到，随着更多祖先A的后代通过与现有成员（此处为C，D或E）共享A作为其MRCA和IBD进入DNA圈，支持祖先作为后代一部分的证据数量 血统可以继续增加。



#### 2.3. 链接远房亲属

与IBD有关的一个相关要点是，即使两个AncestryDNA成员都来自特定祖先，他们也不一定共享任何遗传的IBD DNA（例如，图2.1中的C和E个体）。 由于遗传遗传的随机性，一个人不一定要与一个人的所有近代表亲（尤其是第四表亲及以后的表亲）共享DNA。 **虽然通过血统相同来共享DNA通常是两个人的亲缘关系的证据，但缺乏IBD匹配并不一定意味着缺乏遥远的家谱关系。**



因此，DNA Circles的第三个也是最后一个目标是允许没有相同血统的DNA的亲戚彼此合作。 图2.1也证明了这一目标。 尽管个体C，D和E都从祖先A继承了DNA，但并非所有后代都共享DNA IBD（即个体C和E）。 但是，作为围绕祖先A的关系组的成员，个体C和E可以检查其建议的家谱关系，尽管事实并非IBD匹配。 因此，DNA Circles为AncestryDNA成员提供了识别与他们没有直接共享DNA IBD的遥远亲戚的可能性，但是他们仍然有遗传证据支持他们的亲戚。



### 3. Methods：DNA Circle的构成

首先，我们描述构成DNA环的两个主要组成部分的方法（见图3.1）：
1.在最近血统相同的个体和不同血统的人的血统之间鉴定的最近的共同祖先（MRCA）
2.亲密的家庭团体。(家族树)

<img src="img/DNA3.1.png"  />

#### 3.1. 打过分的最近共祖 Scored Most Recent Common Ancestors (MRCAs)

对于两个具有相同血统DNA的个体（请参阅第2节），我们可以估计将两个个体与其共同祖先分开的世代数。 但是，它们的IBD片段本身并不显示其共同祖先的身份。 每个人的谱系信息使您可以搜索两个人记录的共同祖先。 **但是，即使已识别出MRCA，该祖先实际上也可能不是他们继承其共享DNA的祖先。**



因此，对于在共享DNA IBD的两个人之间识别出的每个MRCA，我们计算一个分数，以量化两个人是否共享DNA IBD，因为他们俩都从发现的MRCA继承了该DNA。



使用三个不同的统计权重的组合来计算分数，每个统计权重都定为介于0和1之间（见图3.2）：
1. W（IBD）：IBD匹配归因于最近的家谱史，
2. W（SharedAncestor）：在两个在线谱系中，所标识的MRCA代表同一个人的可信度，以及
3. W（继承）：由于相关的祖先（而不是来自另一个祖先或来自更远的家谱史），个人具有IBD匹配的置信度。



下面，我们描述了这些权重的推导和计分以及如何将其用于计算MRCA的分数。

![](img/DNA3.2.png)

##### 3.1.1 W(IBD)

个体是否共享IBD？

将DNA样本提交给AncestryDNA时，可以在Illumina Omni-Express平台上获得超过700,000个全基因组标记的基因型（更多信息，请参见种族估计白皮书）。 有了此全基因组数据，AncestryDNA将在所有对AncestryDNA成员之间执行IBD分析。 这可以确定在不久的将来可能从共享的共同祖先那里继承而来的具有长而相同的DNA片段的个体对。 即继承相同的血统（IBD）（见图2.1）。 当一对个体共享足够数量的DNA IBD并被认为是相关的时，即可确定IBD匹配，并且可以通过个体之间的分离程度对其进行分类：即父母/子女，兄弟姐妹，第一堂兄弟等等。



尽管被识别为IBD匹配，但每对个体可能有不同数量的证据表明，它们之间的共享DNA在血统上实际上是相同的（而不是虚假匹配或状态上相同）。 为了反映这一点，我们计算了一个统计值W（IBD），该值介于0和1之间，表示通过最近的共同家谱祖先，IBD匹配归因于相关性的置信度。 随着对AncestryDNA的IBD匹配算法的改进和修改，任意两个成员之间的W（IBD）值可能会随时间变化（请参阅第6节）。



AncestryDNA在所有对的AncestryDNA成员之间执行IBD分析。 这可以识别出在不久的将来可能从一个共同的祖先那里继承而来的具有长而相同的DNA片段的个体对。 即继承相同的血统（IBD）（见图2.1）。 当一对个体共享足够数量的DNA IBD并被认为是相关的时，即可确定IBD匹配，并可以通过个体之间的分离程度对其进行分类：即父母/子女，兄弟姐妹，第一堂兄弟等等。



尽管被识别为IBD匹配，但每对个体可能有不同数量的证据表明，它们之间的共享DNA在血统上实际上是相同的（而不是虚假匹配或状态上相同）。 为了反映这一点，我们计算了一个统计值W（IBD），该值介于0到1之间，表示IBD匹配是由于最近的共同家谱祖先的相关性引起的置信度。 随着对AncestryDNA的IBD匹配算法的改进和修改，任意两个成员之间的W（IBD）值可能会随时间变化（请参阅第6节）。



有关IBD分析，分离程度估计和置信度得分的更详细讨论，请参见《Matching White Paper.》。



##### 3.1.2 W(共祖)

这些人有共同的祖先吗？

如第2节所述，先祖DNA成员通常会建立在线谱系，并将这些谱系与他们的DNA测试相关联（即，识别在线谱系中提交DNA样本的个人）。 这些谱系通常是详细家谱研究的结果，该研究综合了各种历史文献或其他Ancestry.com成员家谱中的信息。



AncestryDNA成员的在线谱系具有不同水平的准确性和完整性。 例如，某些成员关于其家族史的信息可能有限，因此，他们的在线谱系的整个分支都将丢失或未知。 相反，其他人将拥有详细的血统书，跨越多个世代，在附属系中有成千上万已确定的亲戚。



在两个血统之间查找MRCA时，我们仅在每个血统的直系祖先（即父母，祖父母，曾祖父母等）中进行搜索（见图3.3）。 这是因为直系祖先是个人继承DNA的唯一亲戚。 此外，我们仅在两个谱系的最近十代中寻找MRCA。 这是由于以下几个原因：（1）在更远的世代中，客户从某个特定祖先那里继承任何DNA的可能性要小得多； （2）从更远的祖先那里继承的DNA可能不足以表明与其他表亲有共同的血统。 （3）客户血统的准确性和可靠性随着我们过去的发展而下降。



对于每个人的谱系中的所有成对的直系祖先，Ancestry.com使用专有算法来识别两个谱系中可能是同一个人的个体。 在此比较中使用的来自在线谱系的信息包括重要信息和关系。 给定一个谱系的两个节点之间信息的一致性，该算法给出一个分数，量化两个谱系中的祖先是否是同一个人。 在这里，我们将该分数（介于0和1之间）表示为W（SharedAncestor）。 如果有关两个血统的祖先的信息完全匹配，则比较可能会得到W（SharedAncestor）的完美分数1。



比较两个血统书时，我们只考虑最近的共同祖先（MRCA），而不是所有共同祖先。 要了解为什么这很重要，请考虑一下母女关系。 母亲和女儿的整个共同祖先包括母亲和母亲的所有直接祖先。 由于母亲的祖先是冗余信息，因此仅将母亲称为MRCA。



但是，可以在两个谱系的不同行上具有多个MRCA。 在这种情况下，我们将考虑在成员谱系的每一行中都识别出的所有MRCA。 虽然最常见的情况是两个人是一对夫妇的后代，但在许多情况下，血统的两个不同分支上可能会发现不同的共同祖先。 图3.4中的示例说明了两个人，他们的血统中共有四个人，分别是MRCA：A，B，C和D。



鉴于MRCA是使用在线谱系识别的，会员可以对其进行修改或更新其文档，因此会定期重复搜索谱系对之间的共同祖先。 对于每对被识别为IBD匹配的个体，该MRCA搜索结果连同W（SharedAncestor）一起记录并存储，以准备进行DNA Circle分析。



##### 3.1.3 W(继承)

个体是否从MRCA共享相同的DNA？

MRCA分数的第三部分是W（继承）。 在W（继承）的上下文中，我们将每对MRCA对（一对配对的MRCA）视为一个实体，而不是检查单个的MRCA（如W（SharedAncestor）一样）。 这是因为一对夫妻的两个成员都将DNA传给后代，很难区分哪个人在后代之间共享了DNA共享的IBD。 W（继承）对两个人是否从相关的MRCA夫妇继承了IBD片段进行评分。



要了解W（继承）背后的动机，请考虑两个人通过MRCA对在血统上具有相同的DNA共享，而不是两个血统中的一个。 发生这种情况的原因之一是通过配合模式。 在整个人口历史中，通常会发现一个家庭在多个世代中不止一次地与另一个家庭结婚，导致成员谱系可能在两个或多个不同的家庭系中拥有MRCA。



此外，很多客户血统书通常是未被观察到的。 由于种种原因，包括谱系研究令人恐惧的“砖墙”，沿着特定血统的成员祖先可能是未知的。 （大多数成员谱系在其直接直线上有100-200个祖先；请参见第5节和图3.5）。 在这种情况下，即使在两个AncestryDNA成员之间鉴定出MRCA，其IBD可能是从一个或两个谱系中未观察到的一对夫妇继承DNA的结果（参见图3.6）。



为了计算W（继承），它也被缩放为介于0和1之间，我们使用了专有算法，该算法考虑了（1）直线谱系大小，（2）共享祖先对的数量和（3） 共享的MRCA对的子代深度。 这些因素中的每一个都使我们对两个人是否从有问题的MRCA夫妇继承了IBD片段的信心。



#### 3.2 家庭组识别和链接

DNA Circle的第二个基本组成部分是DNA Circle成员本身。 DNA圈的成员既可以是（1）个单独的AncestryDNA成员，也可以是（2）个“家庭组”，这些“家族组”将被推断为家庭一部分的单个AncestryDNA成员进行分组，以结合其非独立的遗传信息。 家庭群体是具有血统证据并推断出IBD的个体的集合，暗示他们是移出或接近的第一代表亲。 由于DNA Circles的各个成员无需进一步讨论，因此本节完全针对家庭群体。



##### 3.2.1 家庭组直观解释

建立家庭团体有两个原因。 首先，一个近亲家族的成员通过血统共享大量相同的DNA。 例如，一个孩子从每个父母那里继承了50％的基因组，从每个祖父母那里继承了大约25％的基因组。 因此，表亲从他们共同的祖父母那里共享其基因组IBD的大约12.5％。 由于IBD数量众多，近亲会提供有关远祖的多余信息。 其次，一个家庭成员通常彼此了解，并且对他们的血统关系充满信心。 正如我们稍后解释的那样（请参见第4节），将密切相关的个人分解为家庭群体，并允许他们作为一个整体与DNA Circle的其他成员建立联系，这使得任何给定的家庭组成员可以比他们更多的DNA Circles连接 单独。



##### 3.2.2 创建家庭组

家庭组是指特定的最新共同祖先。 我们根据IBD与已识别的MRCA的匹配来计算家庭组，其中IBD建议一旦移除或接近，则估计是第一个表亲的关系。 选择该阈值有两个原因：（1）我们希望近亲家族成员在2至3代内保持联系，以保持较高的树准确度（大多数成员都知道其祖父母是谁），（2）分析表明，给定 它们之间存在大量IBD，因此我们在此级别上几乎确定了所有真正的表亲关系（召回率> 99％）。 尽管我们在这个水平上失去了一些先兄弟，但他们的回忆率仍然很高（> 82％）。



我们以一个示例讨论家庭团体的创建。 图3.7显示了具有5个AncestryDNA成员A，B，C，D和E，以及祖先F（不是AncestryDNA成员）的血统书。 表3.1显示了仅在A，B，C和D个人之间进行的AncestryDNA IBD分析得出的示例结果集。



为了创建一个家庭群体，我们考虑每个成对的关系，其中既有IBD则建议有一个表亲，一旦关系被消除或变得更近，也有一个已鉴定的MRCA（见表3.1）。 实际上，检查成对的个人并将其添加到家庭组的顺序是随机的。



将遵循以下步骤来分析这些已识别的IBD匹配并创建一个家庭组。 首先，B和C将以A作为MRCA形成一个家族群，因为据估计，它们与移除后的第一个表亲的亲缘关系更近（见图3.8）。 由于B与D共享IBD，并且具有相同的MRCA（A），因此D被添加到家庭组中。 出于相同的原因，A与B的IBD匹配将A添加到家庭组。 因此，A，B，C和D都属于同一个家庭组。 请注意，仅针对沿A的直系祖先的DNA Circles将这些个体聚合到一个家庭组中。



##### 3.2.3 家庭组之间的联系

有时，我们会确定将一个家庭的成员添加到另一个家庭的家庭组之间的关系，例如，当发现一个家庭的MRCA是另一家庭的后代时。 为了说明起见，请考虑图3.7，其中A有一个姊妹E。A和E将围绕其MRCA（他们的母亲F）创建一个家庭组。 尽管B，C和D都将与E共享IBD，但他们不太可能与E共享足够的IBD成为一个家庭成员（因为一旦被移除，它们与第一堂兄弟的亲戚关系不大）。 但是，由于B，C和D都属于A的家庭，而A属于E的家庭，因此A的家庭将成为F（母亲）的家庭的“子家庭”。



##### 3.2.4 家庭组创建的局限

建立家庭团体有很多限制。 与MRCA的识别一样（请参阅第3.1节），只有当AncestryDNA成员将其样本与其谱系中的一个节点相关联时，才能创建家族组。 如果一个人将他们的样本与树中一个不准确的节点（代表参加AncestryDNA测试的人以外的人）相关联，则会损害家庭关系，进而损害DNA Circles。 与所有与DNA Circles相关的分析一样，树木质量也是一个重要的警告和局限性（请参见第6节）。



### 4. Methods：DNA Circle创建

给定第3节中描述的DNA Circles的组成部分，我们描述了创建DNA Circles和计算相关分数所采取的步骤。



首先，我们介绍加权图或网络的概念，它是可视化和表示DNA Circle的有用方法（请参见图4.1）。 成员（个人和家庭组；请参阅第3.2节）由节点表示，节点之间的加权边是MRCA的得分（e i↔j；请参阅第3.1节）。 使用此框架，我们讨论了如何创建DNA Circles以及如何计算其相关分数（见图4.2）。

![](img/DNA4.1.png)

![](/Users/eyreyoung/Desktop/Notes/Lab/img/DNA4.2.png)



#### 4.1 添加节点和边

我们重申，DNA Circle始终是指特定祖先。 我们汇总了不仅共享IBD而且在同一祖先拥有MRCA的个人对，那里有足够的证据支持该对个人实际上确实从MRCA继承了DNA（请参阅第3.1节）。



对于家庭群体，DNA Circles的构建以类似的方式进行。 给定节点对（家庭组和个人）的列表，它们共享IBD和MRCA，且MRCA得分ei↔j≥t（请参阅第3.1节），我们以任意顺序遍历每对节点。 我们保留每个DNA圈中哪些成员与谁（以及强度如何）相关的记录。 根据定义，DNA Circle必须具有三个或更多节点。 请注意，我们仅围绕所有节点返回小于或等于6代的祖先创建DNA环（即，如果它们的MRCA返回大于6代，则我们将省略节点对）。



遍历每对潜在成员，除了在现有节点上增加节点和边缘外，还会创建新的网络（见图4.3）。 当发现MRCA已经是DNA Circle的头时，我们添加成员。 给定构建DNA环的随机顺序，可以在此过程中合并多个DNA环（请参见图4.3）。 最终的DNA Circle是节点和这些节点之间的加权边的集合。

