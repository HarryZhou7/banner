# banner
banner轮播图


		<div class="banner-bg">
			<div class="banner">
				<span class="pre"></span>
				<span class="next"></span>
				<a href="###" class="first"><img src="../images/banner1.jpg"></a>
				<a href="###"><img src="../images/banner2.jpg" /></a>
				<a href="###"><img src="../images/banner3.jpg" /></a>
				<a href="###"><img src="../images/banner4.jpg" /></a>
				<div class="choose">
					<span class="red"></span>
					<span></span>
					<span></span>
					<span></span>
				</div>
			</div>
		</div>






.banner-bg{
	background: #0e0f16;
	width: 100%;
	height: 320px;
	margin-top: -10px;
}
.banner-bg .banner {
	margin: 0 auto;	
	width: 900px;
	height: 320px;
	position: relative;
	overflow: hidden;
}

.banner-bg .banner a {
	z-index: 100;
	display: block;
	width: 100%;
	height: 100%;
	position: absolute;
	left: 100%;
	top: 0;
}

.banner-bg .banner .first {
	left: 0;
}

.banner-bg .banner a img {
	width: 100%;
	height: 100%;
}

.banner-bg .banner .choose {
	z-index: 1000;
    position: absolute;
    left: 665px;
    top: 289px;
    width: 220px;
    height: 10px;
}

.banner-bg .banner .choose span {
	margin-right: 15px;
	float: left;
	display: block;
	background: rgba(255,255,255,0.5);
	width: 40px;
	height: 10px;
}

.banner-bg .banner .choose span:hover {
	background: #cd1a1d;
}

.banner-bg .banner .choose .red {
	background: #cd1a1d;
}

.banner-bg .banner .pre,
.next {
	cursor: pointer;
	text-align: center;
	display: none;
	width: 42px;
	height: 74px;	
	text-decoration: none;
	z-index: 200;
	display: none;
	position: absolute;
	top: 111px;
}
.banner-bg .banner:hover .pre{
	display: block;
}
.banner-bg .banner:hover .next {
	display: block;
}
.banner-bg .banner .pre {
	left: 0px;
	background-position: 0% 0%;
	background-image: url(banner-icon.png);
}

.banner-bg .banner .next {
	right: 0px;
	background-position: 100% 0%;
	background-image: url(banner-icon.png);
}





$(function() {
	var prePage = null;
	var curPage = null;

	function next() {
		$(".banner-bg .banner a").eq(curPage).stop(true, true).css("left", "100%").animate({
			"left": "0"
		});
		$(".banner-bg .banner a").eq(prePage).stop(true, true).css("left", "0").animate({
			"left": "-100%"
		})
	};

	function pre() {
		$(".banner-bg .banner a").eq(curPage).stop(true, true).css("left", "-100%").animate({
			"left": "0"
		});
		$(".banner-bg .banner a").eq(prePage).stop(true, true).css("left", "0").animate({
			"left": "100%"
		})
	};
	$(".banner-bg .banner .choose span").mouseover(function() {
		curPage = $(this).index();
		$(".banner-bg .banner .choose span").eq(curPage).addClass("red").siblings().removeClass("red");
		if(curPage > prePage) {
			next()
		} else if(curPage < prePage) {
			pre()
		};
		return prePage = curPage;
	});
	$(".banner-bg .banner .next").click(function() {
		curPage++;
		if(curPage > 3) {
			curPage = 0
		};
		$(".banner-bg .banner .choose span").eq(curPage).addClass("red").siblings().removeClass("red");
		next();
		return prePage = curPage;
	});
	$(".banner-bg .banner .pre").click(function() {
		curPage--;
		if(curPage < 0) {
			curPage = 3
		};
		$(".banner-bg .banner .choose span").eq(curPage).addClass("red").siblings().removeClass("red");
		pre();
		return prePage = curPage;
	});
	setInterval(function() {
		$(".banner-bg .banner .next").click()
	}, 3000)

})
