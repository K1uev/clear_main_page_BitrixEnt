Для того, чтобы отредактировать базовые элементы Битрикса (подвал, карточку пользователя, левое и правое меню), можно загрузить имеющиеся файлы или заменить строки кода на те, которые находятся ниже

1. Подвал сайта

Путь к файлу:

local/templates/bitrix24/footer.php

							<!-- !!!ИСПРАВЛЕНО!!! -->
								<span class="bitrix24-copyright"><?=GetMessage("GAZPROM_NAME", array("#CURRENT_YEAR#" => date("Y")))?></span>
								<!-- <?
								if (Bitrix\Main\Loader::includeModule('bitrix24'))
								{
									$licensePrefix = CBitrix24::getLicensePrefix();
									$licenseType = CBitrix24::getLicenseType();
								}

								if ($isBitrix24Cloud && $partnerID = COption::GetOptionString("bitrix24", "partner_id", ""))
								{
									if ($partnerID != "9409443") //sber
									{
										$arParamsPartner = [];
										$arParamsPartner["MESS"] = [
											"BX24_PARTNER_TITLE" => GetMessage("BITRIX24_PARTNER_POPUP_TITLE"),
											"BX24_BUTTON_SEND" => GetMessage("BITRIX24_PARTNER_POPUP_BUTTON"),
										];
										?><a href="javascript:void(0)" onclick="showPartnerForm(<?= CUtil::PhpToJSObject($arParamsPartner) ?>); return false;" class="footer-link"><?=GetMessage("BITRIX24_PARTNER_CONNECT")?></a><?php
									}
								}
								elseif (Bitrix\Main\Loader::includeModule('bitrix24'))
								{
									$orderParams = \CBitrix24::getPartnerOrderFormParams();
									?><a class="b24-web-form-popup-btn-57 footer-link" onclick="B24.showPartnerOrderForm(<?=CUtil::PhpToJSObject($orderParams)?>);"><?=GetMessage("BITRIX24_PARTNER_ORDER")?></a><?
								}
								else
								{
									?>
									<a href="javascript:void(0)" onclick="BX.Helper.show();"
									   class="footer-link"><?=GetMessage("BITRIX24_MENU_CLOUDMAN")?></a><?
								}
								?>
								<span
									class="footer-link"
									onclick="BX.Intranet.Bitrix24.ThemePicker.Singleton.showDialog()"
								><?=GetMessage("BITRIX24_THEME")?></span>
								<?
								?><span
									class="footer-link"
									onclick="window.scroll(0, 0); setTimeout(function() {window.print()}, 0)"
								><?=GetMessage("BITRIX24_PRINT")?></span> -->
								<??>
							</span>

							<!-- !!!ИСПРАВЛЕНО!!! -->

Также необходимо добавить в языковой файл строку, для вывода "«Газпром», 2023"

Путь к файлу:

local/templates/bitrix24/lang/ru/footer.php

$MESS["GAZPROM_NAME"] = "«Газпром», #CURRENT_YEAR#";


2. Правое меню

Путь к файлу:

local/templates/bitrix24/components/bitrix/im.messenger/.default/template.php

<!-- !!!ИСПРАВЛЕНО!!! -->

<div class="bx-im-bar bx-im-bar-with-ol" id="bx-im-bar">
	<!-- <div class="help-block bx-im-border-b" id="bx-help-block" title="<?=GetMessage("AUTH_HELP")?>">
		<div class="help-icon-border"></div>
		<div class="help-block-icon"></div>
		<div class="help-block-counter-wrap" id="bx-help-notify">
		</div>
	</div> -->
	<?
	if ($arResult["SHOW_HELP_SPOTLIGHT"])
	{
		$APPLICATION->includeComponent("bitrix:spotlight", "", array(
			"ID" => "help-spotlight2",
			"USER_TYPE" => "ALL",
			"JS_OPTIONS" => array(
				"targetElement" => "#bx-help-block",
				"content"       => Loc::getMessage("IM_HELP_SPOTLIGHT"),
				"targetVertex"  => "middle-center",
				"left" => -10,
				"lightMode"     => true
			)
		));
	}
	?>
	<div class="bx-im-helper-block bx-im-border-b">
		<div id="bx-im-bar-notify" class="bx-im-informer">
			<div class="bx-im-informer-icon" title="<?=GetMessage('IM_MESSENGER_OPEN_NOTIFY');?>">
				<div class="bx-im-informer-num"></div>
			</div>
		</div>
		<div id="bx-im-bar-ol" class="bx-im-informer bx-im-informer-ol">
			<div class="bx-im-informer-ol-icon" title="<?=GetMessage('IM_MESSENGER_OPEN_OL');?>">
				<div class="bx-im-informer-num"></div>
			</div>
		</div>
	</div>
	<div id="bx-im-bar-search" class="bx-im-search bx-im-border-b" title="<?=GetMessage('IM_MESSENGER_OPEN_SEARCH');?>">
		<div class="bx-im-informer-num"></div>
	</div>
	<div class="bx-im-users-wrap">
		<div class="bx-im-scroll-wrap" id="bx-im-external-recent-list"></div>
	</div>

<!-- !!!ИСПРАВЛЕНО!!! -->

Для изменения цвета правого меню необходимо изменить код стилей

Путь к файлу:

local/templates/bitrix24/components/bitrix/im.messenger/.default/style.css

.bx-im-bar.bx-im-bar-with-ol {
	background: rgb(238, 242, 244);
}

.bx-im-bar-with-ol .bx-im-users-wrap {
	top: 155px;
}

Также, при необходимости, можно заменить базовые иконки (сообщения, открытые линии, оповещения и т. д.)

Загрузить новые иконки в images и добавить пути:

/* Иконки в popup */

/* Сообщения: */

.bx-desktop-tab-icon-im {
	background-image: url(images/Chat.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M12.942.994c1.16%200%202.1.94%202.1%202.1v7.8a2.1%202.1%200%2001-2.1%202.1H6.343L3.95%2015.708a.4.4%200%2001-.7-.264v-2.45H2.154a2.1%202.1%200%2001-2.1-2.1v-7.8c0-1.16.94-2.1%202.1-2.1h10.788zm-.283%201.794H2.477a.7.7%200%2000-.693.605l-.007.095v7.01a.7.7%200%2000.605.694l.095.007h2.197v1.05l.95-1.05h7.035a.7.7%200%2000.694-.605l.006-.095v-7.01a.7.7%200%2000-.7-.7zM5.3%205.952a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3H3.794a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3H5.3zm3.106%200a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3H6.901a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3h1.504zm3.107%200a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3h-1.504a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3h1.504z%22%20fill%3D%22%2393979B%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

.bx-desktop-tab-active .bx-desktop-tab-icon-im,
.bx-desktop-tab:hover .bx-desktop-tab-icon-im {
	background-image: url(images/Chat_active.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M12.942.994c1.16%200%202.1.94%202.1%202.1v7.8a2.1%202.1%200%2001-2.1%202.1H6.343L3.95%2015.708a.4.4%200%2001-.7-.264v-2.45H2.154a2.1%202.1%200%2001-2.1-2.1v-7.8c0-1.16.94-2.1%202.1-2.1h10.788zm-.283%201.794H2.477a.7.7%200%2000-.693.605l-.007.095v7.01a.7.7%200%2000.605.694l.095.007h2.197v1.05l.95-1.05h7.035a.7.7%200%2000.694-.605l.006-.095v-7.01a.7.7%200%2000-.7-.7zM5.3%205.952a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3H3.794a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3H5.3zm3.106%200a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3H6.901a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3h1.504zm3.107%200a.3.3%200%2001.3.3v1.504a.3.3%200%2001-.3.3h-1.504a.3.3%200%2001-.3-.3V6.252a.3.3%200%2001.3-.3h1.504z%22%20fill%3D%22%2317b0e1%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

/* Открытые линии:  */

.bx-desktop-tab-icon-im-ol {
	background-image: url(images/Open_line.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M8.106%2014.177c-2.554-.008-4.873-1.52-5.865-3.826a6.095%206.095%200%20011.254-6.759c1.755-1.77%204.46-2.303%206.823-1.343%202.788%201.153%204.399%204.033%203.865%206.91-.534%202.878-3.067%204.97-6.077%205.018zm6.35-1.56c2.368-3.249%201.84-7.747-1.23-10.472-3.053-2.703-7.69-2.704-10.66-.004-2.985%202.723-3.374%207.22-.905%2010.471%202.442%203.239%206.998%204.152%2010.478%202.102a.531.531%200%2000.1.058l2.165.567a.539.539%200%2000.518-.138.523.523%200%2000.131-.513l-.598-2.07zm-4.282-3.335a.46.46%200%2000-.464-.134.485.485%200%2000-.332.363.543.543%200%2000.134.496l.245.258H5.32a.394.394%200%2000-.378.413l.003.2c-.006.217.169.4.391.412h4.44l-.237.26a.532.532%200%2000-.118.495c.04.17.171.31.344.363a.45.45%200%2000.46-.134l1.038-1.133a.541.541%200%2000-.011-.724l-1.079-1.135zM6.076%206.75a.445.445%200%2000.334-.15.541.541%200%2000-.011-.724l-.245-.258h4.44a.392.392%200%2000.377-.412l-.003-.2a.407.407%200%2000-.391-.412h-4.44l.238-.26a.539.539%200%2000-.013-.722.458.458%200%2000-.674-.002L4.65%204.744a.54.54%200%2000.011.724L5.736%206.6a.46.46%200%2000.34.149zm-.65.71v.001a.392.392%200%2000-.378.412l.003.204c-.006.216.168.4.39.412h5.367a.392.392%200%2000.378-.412l-.004-.202a.408.408%200%2000-.39-.414H5.427z%22%20fill%3D%22%2393979B%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

.bx-desktop-tab-active .bx-desktop-tab-icon-im-ol,
.bx-desktop-tab:hover .bx-desktop-tab-icon-im-ol {
	background-image: url(images/Open_line_active.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M8.106%2014.177c-2.554-.008-4.873-1.52-5.865-3.826a6.095%206.095%200%20011.254-6.759c1.755-1.77%204.46-2.303%206.823-1.343%202.788%201.153%204.399%204.033%203.865%206.91-.534%202.878-3.067%204.97-6.077%205.018zm6.35-1.56c2.368-3.249%201.84-7.747-1.23-10.472-3.053-2.703-7.69-2.704-10.66-.004-2.985%202.723-3.374%207.22-.905%2010.471%202.442%203.239%206.998%204.152%2010.478%202.102a.531.531%200%2000.1.058l2.165.567a.539.539%200%2000.518-.138.523.523%200%2000.131-.513l-.598-2.07zm-4.282-3.335a.46.46%200%2000-.464-.134.485.485%200%2000-.332.363.543.543%200%2000.134.496l.245.258H5.32a.394.394%200%2000-.378.413l.003.2c-.006.217.169.4.391.412h4.44l-.237.26a.532.532%200%2000-.118.495c.04.17.171.31.344.363a.45.45%200%2000.46-.134l1.038-1.133a.541.541%200%2000-.011-.724l-1.079-1.135zM6.076%206.75a.445.445%200%2000.334-.15.541.541%200%2000-.011-.724l-.245-.258h4.44a.392.392%200%2000.377-.412l-.003-.2a.407.407%200%2000-.391-.412h-4.44l.238-.26a.539.539%200%2000-.013-.722.458.458%200%2000-.674-.002L4.65%204.744a.54.54%200%2000.011.724L5.736%206.6a.46.46%200%2000.34.149zm-.65.71v.001a.392.392%200%2000-.378.412l.003.204c-.006.216.168.4.39.412h5.367a.392.392%200%2000.378-.412l-.004-.202a.408.408%200%2000-.39-.414H5.427z%22%20fill%3D%22%2317b0e1%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

/* Оповещения: */

.bx-desktop-tab-icon-notify {
	background-image: url(images/Ring.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2214%22%20height%3D%2215%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M5.338%2012.976l-.002.027a1.713%201.713%200%20003.424%200l-.002-.027h-3.42zm5.976-7.297c0-1.496-1.16-3.618-3.464-4.018v-.038A.852.852%200%20007%20.774a.851.851%200%2000-.849.849v.04c-2.3.402-3.457%202.522-3.457%204.016%200%201.658.017%202.84.017%203.601%200%20.761-1.762%201.837-1.762%201.837v.936h12.11v-.936s-1.761-1.076-1.761-1.837c0-.76.016-1.943.016-3.601z%22%20fill%3D%22%2393979B%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

.bx-desktop-tab-active .bx-desktop-tab-icon-notify,
.bx-desktop-tab:hover .bx-desktop-tab-icon-notify {
	background-image: url(images/Ring_active.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2214%22%20height%3D%2215%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M5.338%2012.976l-.002.027a1.713%201.713%200%20003.424%200l-.002-.027h-3.42zm5.976-7.297c0-1.496-1.16-3.618-3.464-4.018v-.038A.852.852%200%20007%20.774a.851.851%200%2000-.849.849v.04c-2.3.402-3.457%202.522-3.457%204.016%200%201.658.017%202.84.017%203.601%200%20.761-1.762%201.837-1.762%201.837v.936h12.11v-.936s-1.761-1.076-1.761-1.837c0-.76.016-1.943.016-3.601z%22%20fill%3D%22%2317b0e1%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

/* Настройки: */

.bx-desktop-tab-icon-config {
	background-image: url(images/Configs.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2215%22%20height%3D%2215%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M9.032.303l.16%201.793c.219.073.43.16.636.257l1.362-1.177a7.321%207.321%200%20012.39%202.349l-1.154%201.381c.101.203.19.413.267.63l1.796.13c.23.937.278%201.946.105%202.987l-.07.364-1.788.161a5.475%205.475%200%2001-.256.647l1.183%201.369a7.2%207.2%200%2001-2.346%202.388l-1.388-1.16a5.477%205.477%200%2001-.645.269l-.13%201.79-.14.033a7.456%207.456%200%2001-3.21-.01l-.16-1.793a5.558%205.558%200%2001-.636-.257l-1.36%201.178a7.321%207.321%200%2001-2.391-2.35l1.154-1.38a5.562%205.562%200%2001-.268-.63l-1.796-.13a7.402%207.402%200%2001-.105-2.988l.07-.364L2.11%205.63c.075-.208.166-.415.271-.618L1.226%203.675A8.55%208.55%200%20013.584%201.28L4.94%202.414c.2-.11.404-.204.61-.283L5.68.326l.14-.033a7.455%207.455%200%20013.212.01zM6.62%203.848c-1.243.264-2.492%201.514-2.757%202.757a3.649%203.649%200%20004.355%204.354%203.588%203.588%200%20002.757-2.757%203.649%203.649%200%2000-4.355-4.354z%22%20fill%3D%22%2393979B%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
	background-position-x: 6px;
}

.bx-desktop-tab-active .bx-desktop-tab-icon-config,
.bx-desktop-tab:hover .bx-desktop-tab-icon-config {
	background-image: url(images/Configs_active.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2215%22%20height%3D%2215%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M9.032.303l.16%201.793c.219.073.43.16.636.257l1.362-1.177a7.321%207.321%200%20012.39%202.349l-1.154%201.381c.101.203.19.413.267.63l1.796.13c.23.937.278%201.946.105%202.987l-.07.364-1.788.161a5.475%205.475%200%2001-.256.647l1.183%201.369a7.2%207.2%200%2001-2.346%202.388l-1.388-1.16a5.477%205.477%200%2001-.645.269l-.13%201.79-.14.033a7.456%207.456%200%2001-3.21-.01l-.16-1.793a5.558%205.558%200%2001-.636-.257l-1.36%201.178a7.321%207.321%200%2001-2.391-2.35l1.154-1.38a5.562%205.562%200%2001-.268-.63l-1.796-.13a7.402%207.402%200%2001-.105-2.988l.07-.364L2.11%205.63c.075-.208.166-.415.271-.618L1.226%203.675A8.55%208.55%200%20013.584%201.28L4.94%202.414c.2-.11.404-.204.61-.283L5.68.326l.14-.033a7.455%207.455%200%20013.212.01zM6.62%203.848c-1.243.264-2.492%201.514-2.757%202.757a3.649%203.649%200%20004.355%204.354%203.588%203.588%200%20002.757-2.757%203.649%203.649%200%2000-4.355-4.354z%22%20fill%3D%22%2317b0e1%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

/* Новости: */

.bx-desktop-tab-icon-im-lf {
	background-image: url(images/News.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2217%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M12.827%208.658a.1.1%200%2001.07.028l3.208%203.099a.1.1%200%2001.023.108l-.023.036-3.208%203.099a.1.1%200%2001-.17-.072v-2.101H9.733v-1.932l2.994-.001V8.758a.1.1%200%2001.1-.1zm.17-8.629a1%201%200%20011%201v5.998h-1.911V1.952H1.947v9.149h6.444v1.922L1%2013.024a1%201%200%2001-1-1V1.03a1%201%200%20011-1h11.997zM5.339%207.254a.3.3%200%2001.3.3V8.72a.3.3%200%2001-.3.3H3.613a.3.3%200%2001-.3-.3V7.554a.3.3%200%2001.3-.3h1.725zm4.814%200a.3.3%200%2001.3.3V8.72a.3.3%200%2001-.3.3H6.755a.3.3%200%2001-.3-.3V7.554a.3.3%200%2001.3-.3h3.397zM5.338%204.068a.3.3%200%2001.3.3v1.167a.3.3%200%2001-.3.3H3.613a.3.3%200%2001-.3-.3V4.368a.3.3%200%2001.3-.3h1.725zm4.814%200a.3.3%200%2001.3.3v1.167a.3.3%200%2001-.3.3H6.755a.3.3%200%2001-.3-.3V4.368a.3.3%200%2001.3-.3h3.397z%22%20fill%3D%22%2393979B%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
	background-position-x: 7px;
}

.bx-desktop-tab-active .bx-desktop-tab-icon-im-lf,
.bx-desktop-tab:hover .bx-desktop-tab-icon-im-lf {
	background-image: url(images/News_active.svg) !important;
	/* background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2217%22%20height%3D%2216%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M12.827%208.658a.1.1%200%2001.07.028l3.208%203.099a.1.1%200%2001.023.108l-.023.036-3.208%203.099a.1.1%200%2001-.17-.072v-2.101H9.733v-1.932l2.994-.001V8.758a.1.1%200%2001.1-.1zm.17-8.629a1%201%200%20011%201v5.998h-1.911V1.952H1.947v9.149h6.444v1.922L1%2013.024a1%201%200%2001-1-1V1.03a1%201%200%20011-1h11.997zM5.339%207.254a.3.3%200%2001.3.3V8.72a.3.3%200%2001-.3.3H3.613a.3.3%200%2001-.3-.3V7.554a.3.3%200%2001.3-.3h1.725zm4.814%200a.3.3%200%2001.3.3V8.72a.3.3%200%2001-.3.3H6.755a.3.3%200%2001-.3-.3V7.554a.3.3%200%2001.3-.3h3.397zM5.338%204.068a.3.3%200%2001.3.3v1.167a.3.3%200%2001-.3.3H3.613a.3.3%200%2001-.3-.3V4.368a.3.3%200%2001.3-.3h1.725zm4.814%200a.3.3%200%2001.3.3v1.167a.3.3%200%2001-.3.3H6.755a.3.3%200%2001-.3-.3V4.368a.3.3%200%2001.3-.3h3.397z%22%20fill%3D%22%2317b0e1%22%20fill-rule%3D%22evenodd%22%2F%3E%3C%2Fsvg%3E'); */
}

/* Иконки левого меню */

.bitrix24-light-theme .bx-im-informer-icon {
	/* background: url(images/Ring_active.svg) center center no-repeat; */
	/* background: rgba(255, 255, 255, 0.2) url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20width%3D%2214%22%20height%3D%2216%22%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cpath%20d%3D%22M5.047%2014.031c0%20.011-.003.021-.003.031a1.97%201.97%200%200%200%203.938%200c0-.01-.003-.02-.003-.031H5.047zm6.871-8.391c0-1.72-1.334-4.16-3.983-4.62V.976A.98.98%200%200%200%206.958%200a.979.979%200%200%200-.976.976v.046c-2.644.463-3.975%202.9-3.975%204.618%200%201.907.019%203.266.019%204.141S0%2011.893%200%2011.893v1.076h13.924v-1.076S11.9%2010.656%2011.9%209.781s.018-2.234.018-4.141z%22%20fill%3D%22%23FFF%22%20fill-rule%3D%22evenodd%22/%3E%3C/svg%3E") no-repeat center; */
	opacity: .9;
}

.bitrix24-dark-theme .bx-im-informer-icon,
.bitrix24-default-theme .bx-im-informer-icon,
.bx-im-bar-default .bx-im-informer-icon {
	background: url(images/Ring_active.svg) center center no-repeat;
	/* background: rgba(82, 92, 105, .11) url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20width%3D%2214%22%20height%3D%2216%22%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cpath%20d%3D%22M5.047%2014.031c0%20.011-.003.021-.003.031a1.97%201.97%200%200%200%203.938%200c0-.01-.003-.02-.003-.031H5.047zm6.871-8.391c0-1.72-1.334-4.16-3.983-4.62V.976A.98.98%200%200%200%206.958%200a.979.979%200%200%200-.976.976v.046c-2.644.463-3.975%202.9-3.975%204.618%200%201.907.019%203.266.019%204.141S0%2011.893%200%2011.893v1.076h13.924v-1.076S11.9%2010.656%2011.9%209.781s.018-2.234.018-4.141z%22%20fill%3D%22%23525C69%22%20fill-rule%3D%22evenodd%22/%3E%3C/svg%3E") no-repeat center; */
	opacity: .9;
}

.bitrix24-light-theme .bx-im-search:before {
	background: url(images/search.svg) center center no-repeat;
	/* background: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2217%22%20height%3D%2217%22%20viewBox%3D%220%200%2017%2017%22%3E%0A%20%20%3Cpath%20fill%3D%22%23FFFFFF%22%20d%3D%22M1.648%2C6%20C1.648%2C3.597%203.597%2C1.648%206%2C1.648%20C8.403%2C1.648%2010.352%2C3.597%2010.352%2C6%20C10.352%2C8.403%208.403%2C10.352%206%2C10.352%20C3.597%2C10.352%201.648%2C8.403%201.648%2C6%20L1.648%2C6%20Z%20M16.916%2C15.565%20L10.863%2C9.504%20C11.575%2C8.518%2012%2C7.31%2012%2C6%20C12%2C2.687%209.314%2C0%206%2C0%20C2.687%2C0%200%2C2.687%200%2C6%20C0%2C9.313%202.687%2C12%206%2C12%20C7.281%2C12%208.465%2C11.595%209.44%2C10.912%20L15.498%2C16.978%20L16.916%2C15.565%20Z%22/%3E%0A%3C/svg%3E%0A') center center no-repeat; */
	opacity: .9;
}

.bitrix24-dark-theme .bx-im-search:before,
.bitrix24-default-theme .bx-im-search:before,
.bx-im-bar-default .bx-im-search:before {
	background: url(images/search.svg) center center no-repeat;
	/* background: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2217%22%20height%3D%2217%22%20viewBox%3D%220%200%2017%2017%22%3E%0A%20%20%3Cpath%20fill%3D%22%23525C69%22%20d%3D%22M1.648%2C6%20C1.648%2C3.597%203.597%2C1.648%206%2C1.648%20C8.403%2C1.648%2010.352%2C3.597%2010.352%2C6%20C10.352%2C8.403%208.403%2C10.352%206%2C10.352%20C3.597%2C10.352%201.648%2C8.403%201.648%2C6%20L1.648%2C6%20Z%20M16.916%2C15.565%20L10.863%2C9.504%20C11.575%2C8.518%2012%2C7.31%2012%2C6%20C12%2C2.687%209.314%2C0%206%2C0%20C2.687%2C0%200%2C2.687%200%2C6%20C0%2C9.313%202.687%2C12%206%2C12%20C7.281%2C12%208.465%2C11.595%209.44%2C10.912%20L15.498%2C16.978%20L16.916%2C15.565%20Z%22/%3E%0A%3C/svg%3E%0A') center center no-repeat; */
	opacity: .9;
}

.bitrix24-dark-theme .bx-im-informer-ol-icon:before,
.bitrix24-default-theme .bx-im-informer-ol-icon:before,
.bx-im-bar-default .bx-im-informer-ol-icon:before {
	background-image: url(images/Chat_active.svg);
}


3. Левое меню

Путь к файлу:

local/templates/bitrix24/components/bitrix/menu/left_vertical/template.php

<!-- !!!ИСПРАВЛЕНО!!! -->
<?if ($USER->IsAdmin()) { ?>

<div class="menu-favorites-more-btn<?if (empty($arResult["ITEMS"]["hide"])):?> menu-favorites-more-btn-hidden<?endif?>">
	<div class="menu-collapsed-more-btn">
		<span class="menu-favorites-more-icon"></span>
	</div>
	
	<div class="menu-default-more-btn">
		<span
			class="menu-favorites-more-text"
			id="menu-more-btn-text"
		><?=Loc::getMessage("MENU_MORE_ITEMS_SHOW")?></span>
		<span class="menu-favorites-more-icon"></span>
	</div>
	<?if ($isCompositeMode || $sumHiddenCounters <= 0):?>
	<span id="menu-hidden-counter" class="menu-item-index menu-item-index-more menu-hidden-counter" data-counter-value="0"></span>
	<?else:?>
	<span id="menu-hidden-counter" class="menu-item-index menu-item-index-more" data-counter-value="<?=$sumHiddenCounters?>"><?
		?><?=($sumHiddenCounters > 99 ? "99+" : $sumHiddenCounters)
	?></span>
	<?endif;?>
</div>

<div class="menu-extra-btn-box">
	<div class="menu-settings-save-btn"><?=Loc::getMessage("MENU_EDIT_READY_FULL")?></div>

	<!-- <div class="menu-help-btn">
		<span class="menu-help-icon-box">
			<span class="menu-help-icon"></span>
		</span>
		<span class="menu-help-btn-text"><?=Loc::getMessage("MENU_HELP")?></span>
	</div> -->

	<!-- <? if ($arResult["SHOW_SITEMAP_BUTTON"]): ?>
	<div class="menu-sitemap-btn">
		<span class="menu-sitemap-icon-box">
			<span class="menu-sitemap-icon"></span>
		</span>
		<span class="menu-sitemap-btn-text"><?=Loc::getMessage("MENU_SITE_MAP")?></span>
	</div>
	<? endif ?> -->

	<div data-bx-role="settings-container" class="menu-settings-btn">
		<span class="menu-settings-icon-box">
			<span class="menu-settings-icon"></span>
		</span>
		<span class="menu-settings-btn-text"><?=Loc::getMessage("MENU_SETTINGS_TITLE")?></span>
	</div>

	<?
	if (CModule::IncludeModule("bitrix24") && CBitrix24::isInvitingUsersAllowed()):?>
		<div class="menu-invite-employees" onclick="<?=CIntranetInviteDialog::showInviteDialogLink(
				[
					'analyticsLabel' => [
						'analyticsLabel[source]' => 'leftMenu',
					]
				]
		)?>">
			<span class="menu-invite-icon-box"><span class="menu-invite-icon"></span></span>
			<span class="menu-invite-employees-text"><?=Loc::getMessage("BITRIX24_INVITE_ACTION")?></span>
		</div>
	<? endif ?>

	<?
	if ($arResult["SHOW_LICENSE_BUTTON"]):

		$arJsParams = array(
			"LICENSE_PATH" => $arResult["B24_LICENSE_PATH"],
			"COUNTER_URL" => $arResult["LICENSE_BUTTON_COUNTER_URL"],
			"HOST" => $arResult["HOST_NAME"]
		);
		?>
		<div class="menu-license-all-container">
			<span
				class="menu-license-all menu-license-all-collapsed"
				onclick="
					if (BX.getClass('B24.upgradeButtonRedirect'))
						B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
			>
				<span class="menu-license-all-icon"></span>
				<span class="menu-license-all-text"></span>
			</span>
			<?if ($arResult["IS_DEMO_LICENSE"] && !empty($arResult["DEMO_DAYS"])):?>
				<span
					class="menu-license-all menu-license-all-default"
					onclick="
						if (BX.getClass('B24.upgradeButtonRedirect'))
						B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
				>
					<span class="menu-license-all-icon"></span>
					<span class="menu-license-all-text menu-license-demo-text">
						<?=Loc::getMessage("MENU_LICENSE_DEMO", [
							"#NUM_DAYS#" => '<span class="menu-license-all-days">'.$arResult["DEMO_DAYS"].'</span>'
						])?>
					</span>
					<span class="ui-btn ui-btn-xs ui-btn-light-border ui-btn-round ui-btn-themes menu-license-demo-button">
						<?=Loc::getMessage("MENU_LICENSE_BUY")?>
					</span>
				</span>
			<?else:?>
				<span
					class="menu-license-all menu-license-all-default"
					onclick="
						if (BX.getClass('B24.upgradeButtonRedirect'))
							B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
				>
					<span class="menu-license-all-icon"></span>
					<span class="menu-license-all-text"><?=Loc::getMessage("MENU_LICENSE_ALL")?></span>
				</span>
			<?endif?>
		</div>
	<?endif?>
</div>

<? } else { ?>
	
<div class="display_none" style="display: none;">
	<div class="menu-favorites-more-btn<?if (empty($arResult["ITEMS"]["hide"])):?> menu-favorites-more-btn-hidden<?endif?>">
	<div class="menu-collapsed-more-btn">
		<span class="menu-favorites-more-icon"></span>
	</div>
	
	<div class="menu-default-more-btn">
		<span
			class="menu-favorites-more-text"
			
		><?=Loc::getMessage("MENU_MORE_ITEMS_SHOW")?></span>
		<span class="menu-favorites-more-icon"></span>
	</div>
	<?if ($isCompositeMode || $sumHiddenCounters <= 0):?>
	<span id="menu-hidden-counter" class="menu-item-index menu-item-index-more menu-hidden-counter" data-counter-value="0"></span>
	<?else:?>
	<span id="menu-hidden-counter" class="menu-item-index menu-item-index-more" data-counter-value="<?=$sumHiddenCounters?>"><?
		?><?=($sumHiddenCounters > 99 ? "99+" : $sumHiddenCounters)
	?></span>
	<?endif;?>
</div>

<div class="menu-extra-btn-box">
	<div class="menu-settings-save-btn"><?=Loc::getMessage("MENU_EDIT_READY_FULL")?></div>

	<!-- <div class="menu-help-btn">
		<span class="menu-help-icon-box">
			<span class="menu-help-icon"></span>
		</span>
		<span class="menu-help-btn-text"><?=Loc::getMessage("MENU_HELP")?></span>
	</div> -->

	<!-- <? if ($arResult["SHOW_SITEMAP_BUTTON"]): ?>
	<div class="menu-sitemap-btn">
		<span class="menu-sitemap-icon-box">
			<span class="menu-sitemap-icon"></span>
		</span>
		<span class="menu-sitemap-btn-text"><?=Loc::getMessage("MENU_SITE_MAP")?></span>
	</div>
	<? endif ?> -->

	<div data-bx-role="settings-container" class="menu-settings-btn">
		<span class="menu-settings-icon-box">
			<span class="menu-settings-icon"></span>
		</span>
		<span class="menu-settings-btn-text"><?=Loc::getMessage("MENU_SETTINGS_TITLE")?></span>
	</div>

	<?
	if (CModule::IncludeModule("bitrix24") && CBitrix24::isInvitingUsersAllowed()):?>
		<div class="menu-invite-employees" onclick="<?=CIntranetInviteDialog::showInviteDialogLink(
				[
					'analyticsLabel' => [
						'analyticsLabel[source]' => 'leftMenu',
					]
				]
		)?>">
			<span class="menu-invite-icon-box"><span class="menu-invite-icon"></span></span>
			<span class="menu-invite-employees-text"><?=Loc::getMessage("BITRIX24_INVITE_ACTION")?></span>
		</div>
	<? endif ?>

	<?
	if ($arResult["SHOW_LICENSE_BUTTON"]):

		$arJsParams = array(
			"LICENSE_PATH" => $arResult["B24_LICENSE_PATH"],
			"COUNTER_URL" => $arResult["LICENSE_BUTTON_COUNTER_URL"],
			"HOST" => $arResult["HOST_NAME"]
		);
		?>
		<div class="menu-license-all-container">
			<span
				class="menu-license-all menu-license-all-collapsed"
				onclick="
					if (BX.getClass('B24.upgradeButtonRedirect'))
						B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
			>
				<span class="menu-license-all-icon"></span>
				<span class="menu-license-all-text"></span>
			</span>
			<?if ($arResult["IS_DEMO_LICENSE"] && !empty($arResult["DEMO_DAYS"])):?>
				<span
					class="menu-license-all menu-license-all-default"
					onclick="
						if (BX.getClass('B24.upgradeButtonRedirect'))
						B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
				>
					<span class="menu-license-all-icon"></span>
					<span class="menu-license-all-text menu-license-demo-text">
						<?=Loc::getMessage("MENU_LICENSE_DEMO", [
							"#NUM_DAYS#" => '<span class="menu-license-all-days">'.$arResult["DEMO_DAYS"].'</span>'
						])?>
					</span>
					<span class="ui-btn ui-btn-xs ui-btn-light-border ui-btn-round ui-btn-themes menu-license-demo-button">
						<?=Loc::getMessage("MENU_LICENSE_BUY")?>
					</span>
				</span>
			<?else:?>
				<span
					class="menu-license-all menu-license-all-default"
					onclick="
						if (BX.getClass('B24.upgradeButtonRedirect'))
							B24.upgradeButtonRedirect(<?=CUtil::PhpToJSObject($arJsParams)?>)"
				>
					<span class="menu-license-all-icon"></span>
					<span class="menu-license-all-text"><?=Loc::getMessage("MENU_LICENSE_ALL")?></span>
				</span>
			<?endif?>
		</div>
	<?endif?>
</div>
</div>
<? } ?>
<!-- !!!ИСПРАВЛЕНО!!! -->

Также в этом файле необходимо поправить кнопку с классом menu-fav-editable-btn menu-favorites-btn

						<!-- !!!ИСПРАВЛЕНО!!! -->
					<?if (!$USER->IsAdmin()) { ?>
						<span style="display: none;">
					<? } ?>
						<span data-role="item-edit-control" class="menu-fav-editable-btn menu-favorites-btn<?=$editBtnHideClass?>"><?
							?><span class="menu-favorites-btn-icon"></span><?
						?></span>
					<?if (!$USER->IsAdmin()) { ?>
						</span>
					<? } ?>
						<!-- !!!ИСПРАВЛЕНО!!! -->