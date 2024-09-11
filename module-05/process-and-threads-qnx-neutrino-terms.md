  ## Mở đầu
  Để có thể có cái nhìn rõ hơn về các section tiếp theo, chúng ta cần phải có cái nhìn bao quát nhất định về mối quan hệ giữa thread và process. Có rất nhiều blog trên mạng giải thích về vấn đề này, nhưng đa số trong đó đọc **không thể hiểu nổi** vì quá lí thuyết, đây là vấn đề khó khăn vì Threads và Process là các khái niệm về bản chất đã rất trừu trượng của hệ điều hành. May mắn là, có một [bài viết](https://www.qnx.com/developers/docs/6.4.1/neutrino/getting_started/s1_procs.html#Threads_and_processes) giải thích khá dễ hiểu hai khái niệm này, và Section này sẽ **dịch lại bài viết đó**.
  
  ## Process and Threads
  
  Trước khi chúng ta nói về threads, process, time slices, và tất cả các "khái niệm lập lịch" đẹp đẽ khác, thì trước tiên hãy thiết lập một ví dụ để ta có thể liên tưởng được.

  ### Process là một ngôi nhà
  
  Đầu tiên hãy đặt nền móng cho ví dụ liên tưởng của chúng ta đối với threads và process bằng cách sử dụng các vật thể gần gũi mà ta thấy mỗi ngày - một ngôi nhà.
  
  Một ngôi nhà thật sự chỉ là một cái container, với một số thuộc tính của nó (chẳng hạn như không gian diện tích, số lượng phòng ngủ hoặc tương tự).

  Nếu chúng ta nhìn nhận theo hướng này, một ngôi nhà thật sự **không chủ động làm** bất kì thứ gì - nó là một vật thể bị động. Đây thực sự là những gì định nghĩa nên một process, chúng ta sẽ sớm khám phá điều này.

  ### Các người sống trong nhà là các threads

  Những người sống bên trong ngôi nhà là cái **vật thể động** - họ sử dụng các phòng khác nhau, xem TV, nấu ăn, tắm rửa và tương tự như vậy. Chúng ta sẽ sớm thấy một threads hoạt động thực sự như thế nào.
  
  #### Single Thread

  Nếu bạn sống một mình, bạn sẽ biết điều này nghỉa là gì - bạn **biết rằng** bạn có thể **làm bất kì điều gì** mà bạn muốn tại **bất kì lúc nào**, bởi vì không ai khác sống trong nhà, nếu bạn muốn tắm, muốn bật stereo, nấu bữa tối - bất kì điều gì - bạn chỉ việc thực hiện nó.

  #### Multi Thread

  Mọi thứ thay đổi đáng kể khi bạn thêm một người khác vào ở trong nhà. Cho rằng bạn đã kết hôn, vậy nên vợ/chồng của bạn cũng chuyển vào sống chung với bạn. Lúc này bạn không thể cứ thế tiến thẳng vào nhà vệ sinh ở bất kì thời điểm nào nữa; bạn cần kiểm tra trước để chắc chắn rằng vợ/chồng bạn không có trong đó!

  Nếu hai người lớn có trách nhiệm sống chung trong một ngôi nhà, thì bạn có thể "nới lỏng" về việc bảo mật sự riêng tư - bạn biết rằng người lớn còn lại sẽ tôn trọng không gian của bạn, sẽ không cố đốt nhà bếp (cố ý!) và tương tự như vậy.

  Bây giờ, nếu có vài đứa trẻ xuất hiện và xới tung mọi thứ, mọi thứ sẽ trở nên thú vị.

  ### Quay trở lại process và threads

  Giống như việc một ngôi nhà sẽ tốn một diện tích nhất định, một process cũng sẽ chiếm dụng một vùng nhớ nhất định! Và giống như chủ nhà có thể thoải mái đi vào bất kì phòng nào trong nhà mà họ muốn, các thread của một process cũng có quyền truy cập chung vào trong vùng nhớ của process đó. Nếu thread cấp phát một cái gì đó (mẹ đi ra ngoài và mua trò chơi điện tử), tất cả các thread khác có quyền truy cập vào nó (bởi vì nó hiện hữu ở một không gian dùng chung - tức là nó đang ở trong nhà). Tương tự, nếu một process cấp phát một vùng nhớ mới, vùng nhớ này sẽ ngay lập tức khả dụng đối với tất cả các threads. Bí quyết ở đây là nhận biết được bộ nhớ có khả dụng cho tất cả các threads trong process hay không. Nếu có, thì bạn sẽ cần tất cả các thread truy cập **một cách đồng bộ hóa** vào đó. Còn nếu nó không khả dụng cho tất cả, cứ xem như nó chỉ khả dụng cho một thread cụ thể, trong trường hợp này, chúng ta có thể giả sử rằng không cần đồng bộ hóa cho vùng nhớ này, bởi vì thread sẽ không tự làm rối chính nó!

  Chúng ta đều biết trong cuộc sống hàng ngày, mọi thứ sẽ không đơn giản như vậy. Bây giờ chúng ta đã biết về một đặc tính cơ bản (tóm gọn: tất cả mọi thứ đều có thể chia sẻ), hãy xem xét một ví dụ khi mà mọi chuyện trở nên thú vị hơn một chút, và tại sao.

  Sơ đồ bên dưới show cho chúng ta cách mà chúng ta thể hiện các threads và process. Process là vòng tròn, thể hiện cho khái niệm "container" (vùng địa chỉ bộ nhớ), và ba đường ngoằn nghèo chính là các threads. Chúng ta sẽ còn thấy các sơ đồ tương tự thế này xuyên suốt cuốn sách.

  ![img](/images/dpt11.gif)
  <hr>
  
  *process như là một container của các threads*

  ### Mutual Exclusion (Loại trừ tương hỗ)

  Nếu bạn muốn đi tắm, và có một người đang sử dụng phòng tắm, bản sẽ phải chờ. Vậy thread xử lí việc này như thế nào?

  Nó sẽ thực hiện một thứ gì đó gọi là **mutual exclusion** (*không dịch tiếng việt cho term này, vì tiếng anh sẽ dễ nhớ hơn*). Nó có khái niệm khá gần nghĩa với những gì mà chúng ta tưởng tượng khi nói đến nó - một số lượng các threads sẽ tự loại trừ lẫn nhau khi truy cập đến một tài nguyên cụ thể.

  Nếu bạn đang đi tắm, bạn sẽ muốn *loại trừ truy cập* vào phòng tắm. Để làm được điều này, bạn về cơ bản sẽ đi tới phòng tắm và khóa cửa từ bên trong. Bất kì ai cố gắng sử dụng phòng tắm sẽ bị chặn lại bởi khóa cửa. Và khi bạn xong, bạn mở khóa cửa, cho phép một ai khác truy cập vào.

  Đấy là những gì mà thread sẽ làm. Một thread sẽ sử dụng một object được gọi là *mutex* (viết tắt của **mut**ual **ex**clusion). Object này sẽ như là ổ khóa trên cửa - một khi thread sở hữu mutex locked, không một thread nào có thể lấy được mutex, cho tới khi chính chủ sở hữu trả nó lại (mở khóa). Giống như một cái khóa cửa, các thread đang chờ lấy mutex sẽ bị chặn lại.

  Một điểm tương đồng thú vị giữa mutex và khóa cửa là việc mutex thật sự chỉ là ổ khóa "khuyến nghị". Nếu một thread không thuân thủ việc sử dụng mutex, thì sự bảo vệ này sẽ trở nên vô dụng. Nếu xét đến ví dụ ngôi nhà của chúng ta, thì việc này giống như một người cố ý phá và xông vào phòng tắm thông qua một bức tường và bỏ qua sự hiện diện của cửa và ổ khóa.

  ### Priorities (Độ ưu tiên)

  Chuyện gì xảy ra nếu phòng tắm đang bị khóa và có một số lượng người đang chờ để được sử dụng nó ? Tất nhiên, tất cả mọi người sẽ đứng đợi ở bên ngoài, chờ cho bất kì ai đang ở trong phòng tắm đi ra ngoài. Câu hỏi thực sự là, "chuyện gì xảy ra tiếp theo khi cửa mở? Ai sẽ là người vào trong tiếp theo?"

  Bạn có thể sẽ suy luận rằng, sẽ là "công bằng" khi cho người chờ lâu nhất vào tiếp theo. Hoặc có thể sẽ là "công bằng" nếu cho người già nhất, hoặc cao nhất, hoặc quan trọng nhất ... Có rất nhiều cách để định nghĩa thế nào là "công bằng" trong trường hợp này.

  Chúng ta giải quyết vấn đề này với các threads thông qua hai yếu tố: *độ ưu tiên* và *thời gian chờ đợi*.

  Giả sử  hai người đi đến nhà tắm (đang khóa) cùng một lúc. Một trong hai đang bị áp lực về deadline (họ đã trễ trong một cuộc họp) trong khi đó người còn lại thì không. Chẳng phải sẽ có lý nếu chúng ta cho phép người đang gấp được vào trước? Well, tất nhiên là có. Câu hỏi quan trọng duy nhất ở đây là cách chúng ta quyết định ai là người quan trọng. Điều này có thể được thực hiện bằng cách gán một độ ưu tiên (hãy sử dụng một con số kiểu như - 1 là độ ưu tiên thấp nhất và 255 là độ ưu tiên cao nhất). Người đang chờ trong ngôi nhà và đang bị áp lực về deadline sẽ có *số ưu tiên cao hơn*, còn người còn lại sẽ có *số ưu tiên thấp hơn*.

  Điều tương tự xảy ra với threads. Một thread sẽ kế thừa thuật toán lập lịch từ thread parent của nó, nhưng có thể gọi hàm [pthread_setschedparam()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/p/pthread_setschedparam.html) để thay đổi chính sách lập lịch và mức độ ưu tiên của nó (nếu nó có quyền làm vậy).

  Nếu một lượng các thread đang chờ, và mutex đã unlocked, chúng ta sẽ đưa mutex cho thread đang chờ có độ ưu tiên cao nhất. Giả sử, bằng cách nào đó, cả hai người có *cùng một độ tiên*. Bây giờ chúng ta sẽ làm gì? Well, trong trường hợp đó, sẽ "công bằng" nếu cho phép người đã chờ lâu hơn được vào tiếp theo. Trong trường hợp có một danh sách các threads đang chờ, thì chúng ta sẽ xét *độ ưu tiên* trước tiên và tiếp là *thời gian chờ đợi*.

  Mutex chắc chắn không phải object đồng bộ hóa duy nhất mà chúng ta gặp phải. Hãy xem xét một vài đối tượng khác.

  ### Semaphores (Cờ hiệu)
  
  Hãy di chuyển từ phòng tắm đến nhà bếp, vì phòng tắm là địa điểm được xã hội chấp nhận để có nhiều người cùng một lúc. Trong nhà bếp, bạn có thể không muốn có *tất cả mọi ngườ* tại đó cùng một lúc. Thực tế, bạn có lẽ muốn giới hạn số lượng người có thể hiện hữu trong nhà bếp.

  Xem như, bạn không bao giờ muốn có trên hai người trong nhà bếp cùng một lúc. Bạn có thể thực hiện với mutex không? Với cách chúng ta đã định nghĩa phía trên thì không khả thi. Tại sao? Đây thực tế là một vấn đề rất thú vị cho ví dụ của chúng ta. Hãy phân tích nó ra thành các bước sau:

  #### Semaphore với count = 1

  Phòng tắm có thể có một trong hai tình huống, với hai trạng thái có thể đi đôi với nhau:

  - **Phòng tắm không khóa** và **Không có ai**.
  - **Phòng tắm khóa** và **Có người**.
  
  Còn lại không còn cách kết hợp nào khả thi - cửa không thể nào khóa nếu không có ai bên trong (chúng ta sẽ mở khóa như thế nào?), và cửa không thể mở khóa nếu một người đang ở trong phòng tắm (làm sao mà họ có được sự riêng tư nếu làm như vậy?). Đây là một ví dụ của việc semaphore với bộ đếm là một - có nhiều nhất một người trong phòng, hay một thread đang sử dụng semaphore.

  Mấu chốt ở đây là cách chúng ta mô tả ổ khóa. Với ổ khóa thông thường cho phòng tắm, bạn chỉ có thể mở khóa từ bên trong - không có một chìa khóa nào cho phép truy cập từ bên ngoài. Thực tế, điều này có nghĩa là việc sở hữu mutex là một thao tác *atomic* - *Không có khả năng* nào để mà khi bạn đang trong quá trình lấy mutex thì có một thread cũng lấy nó, dẫn đến việc cả hai đều có mutex. Trong ví dụ ngôi nhà của chúng ta, điều này ít rõ ràng hơn vì con người thông minh hơn rất nhiều so với các con số 0 và 1.

  Vì thế, thứ chúng ta cần cho nhà bếp sẽ là một loại ổ khóa khác.

  #### Semaphore với count > 1

  Giả sử bây giờ, chúng ta đã thiết lập *một ổ khóa có chìa* truyền thống cho nhà bếp. Cách hoạt động của ổ này là nếu bạn có chìa khóa, bạn có thể mở cửa và bước vào trong. Bất kì ai sử dụng ổ khóa này sẽ cam kết rằng, khi họ bước vào bên trong, họ sẽ ngay lập tức khóa cửa lại từ bên trong và vì thế bất kì ai bên ngoài bước vào sẽ luôn cần có chìa khóa.

  Well, bây giờ, vấn đề trở nên đơn giản là làm sao để quy định bao nhiều người chúng ta muốn có trong nhà bếp - treo hai cái chìa khóa bên ngoài cửa! Nhà bếp luôn luôn khóa! Khi một người muốn vào nhà bếp, họ sẽ thấy nếu có chìa khóa được treo ngoài đó. Như vậy, họ có thể sử dụng chìa này, mở cửa nhà bếp, đi vào và khóa cửa lại từ bên trong.

  Vì người vào trong bếp phải có chìa khóa, cho nên chúng ta kiểm soát một cách trực tiếp số lượng người được phép vào nhà bếp tại bất kì thời điểm nào bằng cách giới hạn số lượng chìa khóa được treo bên ngoài cửa.

  Với threads, điều này thực hiện thông qua một *semaphore*. Một semaphore "đơn thuần" thì sẽ hoạt động giống như mutex - hoặc là bạn sở hữu nó, nghĩa là bạn đã truy cập vào tài nguyên, hoặc là không sở hữu nó, nghĩa là bạn không truy cập. Semaphore mà chúng ta mô tả trong ví dụ nhà bếp là một *counting semaphore* - nó theo dõi số lượng (bằng số lượng chìa khóa khả dụng cho các threads).

  #### Một semaphore đóng vai trò như là một mutex

  Chúng ta vừa trả lời cho câu hỏi "Bạn có thể thực hiện nó với một mutex?" trong tình huống implement một ổ khóa với bộ đếm, và câu trả lời là không. Vậy còn tình huống ngược lại thì sao? Liệu chúng ta có thể sử dụng semaphore như một mutex?
  
  Có. Trong thực tế, trong một số hệ điều hành, đó chính xác là những gì chúng làm - chúng không có mutex, mà chỉ có semaphore! Vậy tại sao phải bận tâm đến mutex làm gì?

  Để trả lời câu hỏi này, nhìn vào ví dụ phòng vệ sinh. Làm thế nào mà người xây dựng ngôi nhà implement "mutex"? Tôi đoán rằng là do bạn không có chìa khóa để treo trên tường!

  Các mutex là **một dạng semaphore cho mục đích đặc biệt**. Nếu bạn muốn muốn chỉ có một thread được phép chạy trên một một phần code nào đó, mutex hiện tại vẫn là cách implement hiệu quả nhất.

  Tiếp theo, chúng ta sẽ tiếp tục xem xét các cơ chế đồng bộ hóa khác - gọi là *condvars*, *barriers* và *sleepons*.

  > Để không bị confuse, hãy nhìn vào việc một mutex có các thuộc tính khác, chẳng hạn như tính kế thừa, và điều này làm nó khác biệt so với một semaphore.

  ## Vai trò của Kernel
  
  Phép ẩn dụ về ngôi nhà thực sự rất tuyệt vời để truyền tải khái niệm về đồng bộ hóa, nhưng nó có một điểm hạn chế lớn. Trong ngôi nhà của chúng ta, có nhiều luồng (threads) chạy đồng thời. Tuy nhiên, trong một hệ thống thực tế, thường chỉ có một CPU, vì vậy chỉ có một "thứ" có thể chạy tại một thời điểm.

  ### Một CPU đơn lẻ

  Hãy xem xét những gì diễn ra ở thực tế, và đặc biệt là trong trường hợp "kinh tế" khi chúng ta chỉ có một CPU trong hệ thống. Trong trường hợp này, vì chỉ có một CPU hiện diện, chỉ có một thread có thể chạy ở bất kì thời điểm nào. Kernel sẽ quyết định (sử dụng một số luật, mà chúng ta sẽ xem xét sơ bộ) thread nào sẽ được chạy, và chạy nó.

  ### Nhiều CPU (SMP)

  Nếu bạn mua một hệ thống có nhiều CPU giống nhau, tất cả đều chia sẻ bộ nhớ và các thiết bị, bạn sẽ có một SMP (SMP viết tắt của Symmetrical Multi Processor, với "symmetrical" chỉ ra rằng tất cả các CPU trong hệ thống đều giống nhau). Trong trường hợp này, số lượng thread có thể chạy đồng thời bị giới hạn bởi số lượng CPU. (Thực tế, điều này cũng đúng với hệ thống có một CPU duy nhất!) Vì mỗi CPU chỉ có thể thực thi một thread tại một thời điểm, nên với nhiều CPU, nhiều thread có thể thực thi đồng thời.

  Hãy tạm thời bỏ qua số lượng CPU có trong hệ thống — một cách trừu tượng hữu ích là thiết kế hệ thống như thể nhiều thread thực sự đang chạy đồng thời, ngay cả khi điều đó không hoàn toàn chính xác. Trong phần ["Những điều cần lưu ý khi sử dụng SMP"](https://www.qnx.com/developers/docs/6.4.1/neutrino/getting_started/s1_procs.html#smpbeware), chúng ta sẽ thấy một số tác động không trực quan của SMP.

  ### Kernel như là một trọng tài

  Vậy ai là người quyết định thread nào sẽ được chạy tại một thời điểm? Đó là nhiệm vụ của kernel.

  Một kernel sẽ quyết định thread nào sẽ sử dụng CPU tại một thời điểm cụ thể, và *chuyển ngữ cảnh* (context) sang thread đó. Hãy phân tích Kernel làm gì với CPU.

  Một CPU có một số lượng các thanh ghi (số lượng chính xác dựa vào processor family). Khi một thread đang chạy, thông tin sẽ được lưu trữ vào các thanh ghi đó (chẳng hạn, vị trí của chương trình).

  Khi mà kernel quyết định một thread khác nên được chạy, nó sẽ cần:
  
  - Lưu lại các thanh ghi của thread đang chạy và các thông tin context khác.
  - Tải các thanh ghi của thread mới và context của thread đó vào CPU.
  
  Nhưng làm thế nào mà kernel quyết định rằng một thread nên chạy? Nó xem xét liệu một thread cụ thể có khả năng sử dụng CPU vào thời điểm hiện tại hay không. Ví dụ, khi chúng ta nói về mutex, chúng ta đã giới thiệu cơ chế blocking state (điều này xảy ra khi một thread sở hữu mutex và một thread khác cũng muốn lấy nó; thread thứ hai sẽ bị chặn).

  Theo cách nhìn nhận của kernel, vì thế, chúng ta có một thread *có thể* tiêu thụ CPU và một thread *không thể*, bởi vì nó bị block và đang chờ mutex. Trong trường hợp này, kernel sẽ để thread có thể chạy tiêu thụ CPU, và đặt list còn lại vào một danh sách nội bộ (nhờ đó kernel có thể theo dõi yêu cầu của nó đối với mutex).

  Rõ ràng đó không phải là một tình huống thú vị. Giả sử rằng có một số lượng các threads *có thể* sử dụng CPU. Nhớ rằng chúng ta ủy quyền việc truy cập vào mutex dựa vào **độ ưu tiên** và **thời gian chờ đợi**? Kernel sử dụng một cơ chế tương tự đễ quyết định xem thread nào sẽ được chạy tiếp theo. Có hai yếu tố: *độ ưu tiên* và *thuật toán lập lịch*, được đánh giá theo thứ tự đó.

  #### Độ ưu tiên

  Xem xét hai threads có khả năng sử dụng CPU. Nếu các threads này có độ ưu tiên khác nhau, thì câu trả lời khá đơn giản - kernel đưa CPU cho thread có độ ưu tiên cao hơn, như cái cách chúng ta đã nói đến trong trường hợp nhận mutex. Lưu ý là độ ưu tiên 0 được dự trù cho idle thread - bạn không thể sử dụng nó.

  Nếu một thread khác với độ ưu tiên cao hơn bỗng dưng có khả năng cần phải sử dụng CPU, kernel sẽ ngay lập tức context-switch đến thread có độ ưu tiên cao hơn. Chúng ta gọi cơ chế này là *preemption* (quyền ưu tiên) - thread có độ ưu tiên cao hơn sẽ chiếm quyền của thread có độ ưu tiên thấp hơn. Khi mà thread có quyền ưu tiên cao hơn hoàn thành, và kernel context thực hiện context-switch lại cho thread có độ ưu tiên thấp hơn đang chạy trước đó, chúng ta gọi cơ chế này là *resumption* (nối lại) - kernel tiếp tục chạy thread trước đó.

  Bây giờ, gải sử rằng hai thread có khả năng sử dụng CPU có cùng một độ ưu tiên.

  #### Thuật toán lập lịch

  Hãy giả sử rằng, một trong các thread đang sử dụng CPU. Chúng ta sẽ nghiên cứu các luật mà kernel sử dụng để quyết định context-switch trong trường hợp này. (Tất nhiên, toàn bộ quá trình này thật sự áp dụng cho các threads có cùng một độ ưu tiên - nếu *trong một khoảng khắc*, nếu mọt thread *có độ ưu tiên cao hơn*  sẵn sàng để sử dụng CPU, nó sẽ lấy nó; đấy là toàn bộ lí do cho việc có tính ưu tiên trong một hệ điều hành thời gian thực.)

  Hai thuật toán lập lịch (policies) mà Neutrino kernel có thể hiểu là Round Robin (hoặc "RR") và FIFO (First-In, First-Out).

  #### FIFO

  Trong thuật toán lập lịch FIFO, một thread được phép tiêu thụ CPU tronng thời gian mà nó muốn. Điều này có nghĩa là, nếu thread đang thực hiện một tác vụ tính toán toán học cực kì lâu, và không một thread nào khác có quyền cao hơn đang sẵn sàng, thì thread đó có khả năng sẽ *được phép chạy vĩnh viễn*. Vậy còn các threads khác có độ ưu tiên ngang bằng thì sao? Chúng cũng bị chặn luôn (tất nhiên bao gồm cả các thread có độ ưu tiên thấp hơn).

  Nếu thread đang chạy quits hoặc *tự nguyện từ bỏ CPU*. *thì* kernel sẽ tìm kiếm các thread có cùng độ ưu tiên mà có khả năng sẽ sử dụng CPU. Nếu không có thread nào như vcậy, *thì* kernel tìm kiếm các thread có độ ưu tiên thấp hơn có khả năng sử dụng CPU. Lưu ý rằng định nghĩa *tự nguyện từ bỏ CPU* có thể có hai nghĩa. Nếu thread vào trạng thái ngủ, hoặc bị chặn bởi một semaphore, tương tự vậy, thì tất nhiên, các thread có độ ưu tiên thấp hơn có thể chạy (như đã mô tả phía trên). Nhưng cũng có một lệnh gọi "đặc biệt", [sched_yeld()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/s/sched_yield.html) (*không cần thiết nhắc đến ở đây*) mà chỉ từ bỏ CPU cho các thread khác có cùng độ ưu tiên -  thread có độ ưu tiên thâp hơn sẽ không bao giờ có cơ hội được chạy nếu một thread có độ ưu tiên cao hơn sẵn sàng được chạy. Nếu một thread thực sự gọi [sched_yeld()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/s/sched_yield.html), và không có một thread nào có cùng độ ưu tiên đang sẵn sàng để chạy, thì thread gốc sẽ tiếp tục được chạy. Lời gọi [sched_yeld()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/s/sched_yield.html) thực tế được sử dụng để cho phép một thread khác có cùng độ ưu tiên bẻ khóa CPU.

  Ở sơ đồ phía dưới, chúng ta thấy có ba threads đang thực thi trong hai process khác nhau.

  ![img](/images/dpt12a.gif)
  <hr>

  *Ba threads đang chạy trong hai process khác nhau*

  Nếu chúng ta giả sử rằng thread "A" và "B" đang READY, và thread "C" đang bị block (có lẽ là đang chờ mutex), và có một thread D (không được hiển thị) đang được chạy, thì đây sẽ là một phần của hàng đợi READY mà Neutrino Kernel duy trì:
  <hr>

  ![img](/images/dpt12b.gif)
  <hr>

  *Hai threads trên hàng đợi READY, một bị block, một đang chạy*

  Sơ đồ này cho thấy hàng đợi READY nội bộ của kernel trông như thế nào, đây là thứ kernel sẽ dùng để lập lịch thread tiếp theo. Lưu ý rằng thread "C" không phải là một phần của hàng đợi, bởi vì nó bị block, và thread "D" cũng không nằm trên hàng đợi này vì nó *đang chạy*.

  #### Round Robin
  Thuật toán lập lịch RR giốntg hệt FIFO, *ngoại trừ việc* thread sẽ không chạy mãi mãi nếu có một thread khác có cùng độ ưu tiên. Nó chỉ chạy trong các khoảng thời gian (*timeslice*) mà hệ thống đã quy định sẵn bằng cách sử dụng các hàm [sched_rr_get_interval()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/s/sched_rr_get_interval.html). Timslice thuờng là 4 ms, nhưng nó thực ra là gấp 4 lần *ticksize*, thông số mà có thể được truy vấn hoặc cài đặt với [ClockPeriod()](https://www.qnx.com/developers/docs/6.4.1/neutrino/lib_ref/c/clockperiod.html).

  Những gì sẽ xảy ra là kernel bắt đầu một RR thread, và đánh dấu lại thời gian. Nếu RR Thread chạy được một lúc, thời gian dành cho nó sẽ hết (timeslice hết). Kernel sẽ kiểm tra xem nếu có một thread nào đó khác có cùng một độ ưu tiên đang ready. Nếu có, kernel sẽ chạy nó. Nếu không, kernel sẽ tiếp tục chạy RR thread (tức là kernel cấp cho thread này một timeslice khác).

  ##### Quy tắc
  
  Tóm tắt lại quy tắc lập lịch (cho một CPU đơn lẻ), theo thứ tự quan trọng:
  
  - Chỉ một thread chạy tại một thời điểm.
  - Thread có độ ưu tiên cao nhất sẽ chạy.
  - Thread sẽ chạy cho tới khi nó bị block hoặc exit.
  - Một RR thread sẽ chạy trong khoảng thời gian nhất định, và sau đó kernel sẽ tái lập lịch cho nó (nếu cần thiết).

  Sơ đồ bên dưới thể hiện các quyết định mà kernel sẽ thực hiện:

  ![img](/images/dpt1.gif)

  Đối với hệ thống nhiều CPU, các luật cũng tương tự, ngoại trừ việc nhiều CPU sẽ có thể chạy nhiều thread đồng thời. Thứ tự các thread chạy (các threads nào sẽ chạy trên các CPUs) sẽ được xác định giống hệt với cách quyết định trên một CPU đơn lẻ - thread READY có độ ưu tiên cao nhất sẽ chạy trên một CPU. Khi xử lý các thread có độ ưu tiên thấp hơn hoặc đã chờ đợi lâu, kernel có thể linh hoạt trong việc lập lịch để tránh lãng phí tài nguyên, đặc biệt là bộ nhớ đệm (cache). Kernel sẽ cố gắng tối ưu hóa việc sử dụng bộ nhớ đệm bằng cách sắp xếp các thread sao cho dữ liệu mà các thread này cần đã sẵn có trong cache hoặc dễ dàng truy cập. Điều này giúp giảm thiểu việc cache miss (khi dữ liệu cần thiết không có trong cache) và tăng hiệu quả xử lý của CPU.

  ### Kernel states
  Chúng ta đã nói về "running", "ready" và "blocked" một cách lỏng lẻo - bây giờ hãy chính thức hóa các *thread states* này.

  #### RUNNING
  State RUNNING đơn giản có nghĩa là thread này bây giờ đang tiêu thụ CPU. Trong hệ thống SMP, sẽ có nhiều threads cùng chạy; trên hệ thống một processor đơn lẻ, sẽ có một thread đang chạy.

  #### READY
  READY state nghĩa là thread có thể chạy ngay bây giờ - ngoại trừ việc là nó không thể, bởi vì có một thread khác (có cùng hoặc có độ ưu tiên cao hơn) đang chạy. Nếu hai thread đều có khả năng sử dụng CPU, một thread có độ ưu tiên 10 và một thread có độ ưu tiên 7, thì thread có độ ưu là 10 sẽ RUNNING còn thread có độ ưu tiên 7 sẽ READY.

  #### Các trạng thái blocked
  Tại sao chúng ta gọi chung là là blocked state? Vấn đề là, không chỉ có *một* block state, mà có hơn hàng chục trạng thái blocking.

  Tại sao lại nhiều thế? Bởi vì Kernel cần theo dõi *tại sao* thread lại bị blocked.

  Chúng ta đã thấy hai blocking state - khi một thread bị block và đang chờ mutex, thread đó đang ở MUTEX state. Khi một thread đang bị block và chờ một semaphore, thì là SEM state. Những trạng thái này đơn giản sẽ giúp chỉ ra hàng đợi nào (và tài nguyên nào) mà thread đó đang bị block.

  Nếu có một số lượng nhất định các threads bị block bởi một mutex (hay nói cách khác là đang trong MUTEX state), chúng sẽ không được kernel quan tâm *cho đến khi* thread sở hữu mutex trả nó lại. Tại thời điểm đó, tất cả các thread đang blocked sẽ trở nên READY, và kerneel sẽ tiến hành tái lập lịch (nếu cần thiết).

  Tại sao là "nếu cần thiết?" Thread mà vừa trả lại mutex rất có thể vẫn có một số thứ khác cần phải làm *và* thread đó có độ ưu tiên cao hơn so với các thread đang chờ. Trong trường hợp này, chúng ta đến với luật thứ hai, "Thread có độ ưu tiên cao nhất sẽ chạy", nghĩa là thứ tự lập lịch không cần phải thay đổi - thread có độ ưu tiên cao vẫn tiếp tục chạy kể cả sau khi đã release mutex.

  ## Quay trở lại với Threads và Process
  Hãy cùng quay trở lại với thảo luận của chúng ta về process và threads trước đó, lần này là với góc nhìn trên một hệ thống thực tế. Sau đó, chúng ta sẽ xem xét về các lợi gọi hàm được sử dụng để xử lí cho threads và process.

  Chúng ta biết rằng một process có thể có một hoặc nhiều threads (Một process không có threads nào thì sẽ không thể *làm* bất cứ thứ gì - Không có ai ở nhà, vậy nên không có gì xảy ra). Hệ thống Neutrino có thể có một hoặc nhiều process. (Tương tự, một hệ thống không có process nào cũng không thể thực hiện bất kì thứ gì)

  Vậy những process và threads này sẽ làm gì? Cuối cùng, chúng cấu thành nên một *hệ thống* - tập hợp các threads và process để thực hiện một mục đích gì đó.

  Ở tầng cao nhất, thì một hệ thống là cấu thành nên từ nhiều process. Mỗi process chịu trách nhiệm cho việc cung cấp một dịch vụ nào đó - có thể là hệ thống tệp (filesystem), trình điều khiển hiển thị (display driver), mô-đun thu thập dữ liệu (data acquisition module), mô-đun điều khiển (control module), hoặc bất kỳ dịch vụ nào khác.

  Bên trong mỗi process, có thể có một số lượng nhất định các threads. Các số lượng này là khác nhau. Một người thiết kế *sử dụng một thread* có thể tạo nên *cùng một chức năng* với một người thiết kế khác *sử dụng năm thread*. Một số vấn đề có thể dễ dàng được giải quyết bằng cách sử dụng đa luồng (multi-threaded) và thực sự khá đơn giản để thực hiện, trong khi các process khác lại phù hợp hơn với việc sử dụng một luồng đơn (single-threaded) và rất khó để chuyển đổi sang đa luồng.

  ### Tại sao lại phải có nhiều process?
  Vậy tại sao không thể có một process với hàng triệu threads? Mặc dù một số hệ điều hành ép buộc chúng ta code theo cách đó, thì việc chia nhỏ công việc ra thành nhiều process có rất nhiều lợi ích về:

  - Tính tách rời và tính mô đun hóa
  - Khả năng bảo trì.
  - Độ tin cậy.

  Khả năng "chia nhỏ vấn đề" ra thành nhiều vấn đề độc lập là một khái niệm mạnh mẽ.