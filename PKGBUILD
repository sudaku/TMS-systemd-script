# Maintainer: Nitroretro <nitroretro@protonmail.com>

# Based on the `minecraft-server` AUR package by:
## Maintainer: Gordian Edenhofer <gordian.edenhofer@gmail.com>
## Contributor: Philip Abernethy <chais.z3r0@gmail.com>
## Contributor: sowieso <sowieso@dukun.de>

_game="sponge"
_server_root="/srv/sponge"

_minecraft_ver=1.12.2
_pkgver=${_minecraft_ver}-1.0.1

pkgname=sponge-server
pkgver=${_pkgver//-/_}
pkgrel=1
pkgdesc="Minecraft Sponge server unit files, script, and jar"
arch=('any')
url="https://minecraftforge.net/"
license=('custom')
depends=('java-runtime-headless=8' 'screen' 'sudo' 'bash' 'awk' 'sed')
optdepends=("tar: needed in order to create world backups"
	"netcat: required in order to suspend an idle server")
backup=("etc/conf.d/${_game}")
install="${pkgname}.install"
source=(
	"${_game}d-backup.service"
	"${_game}d-backup.timer"
	"${_game}d.service"
	"${_game}d.conf"
	"${_game}d.sh"
	"LICENSE.txt")
sha512sums=('127daad73d2c4505b7844c776147c31ec78349877f7a91892e738c7b2e36f6ea1a405d39b33a5b8559683fec979bf83d8d78255288944cc7a075649d43e6b84b'
            'bfeb936a77b00eca3812ee2e8e0cc7fcc9b4e67dc25c0bc14c883cfabbaf84d4697a811cc1dab42b1c03cb6b4f7765c287556d47e7942adc51d0066c454c849b'
            'b7f90c79cdcc5edf8385a66fac223c988c2cbe28299068014f4fec3c88a6e6fb25875667c398a700e69fcd788ae1dc6c774c0e46a48b0aad50431e8fb9309ef4'
            '170d748169572de5e868c63fb6f19402cdf82404e2bacf8a5e39b547c1740ffa41924261b03e64c245af253b0dcfce27f90f94dcff5fe17bc1e688a0f0265dd8'
            '8723ccb98e0d95c0006e56f36a4d507a83a9978605e14765ab432efc0967f41e43c5ca66b6030875261de6d258bb514a7ebf0db3843965456e51d3c8b8fee909'
            '3da10d63a5edee4bc8bcd3d5c2730771062f7fa58626a8c51635fbe96bfbceca3ff6937cfaad3e17f16a94ef95137f7c78cc6dac1c846a6b9a8f18d3c6355973')

package() {
	install -Dm644 "LICENSE.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"

	install -Dm644 "${_game}d.conf"                         "${pkgdir}/etc/conf.d/${_game}"
	install -Dm755 "${_game}d.sh"                           "${pkgdir}/usr/bin/${_game}d"
	install -Dm644 "${_game}d.service"                      "${pkgdir}/usr/lib/systemd/system/${_game}d.service"
	install -Dm644 "${_game}d-backup.service"               "${pkgdir}/usr/lib/systemd/system/${_game}d-backup.service"
	install -Dm644 "${_game}d-backup.timer"                 "${pkgdir}/usr/lib/systemd/system/${_game}d-backup.timer"

	# Link the log files
	mkdir -p "${pkgdir}/var/log/"
	install -dm2755 "${pkgdir}/${_server_root}/logs"
	ln -s "${_server_root}/logs" "${pkgdir}/var/log/${_game}"

	# Give the group write permissions and set user or group ID on execution
	chmod g+ws "${pkgdir}${_server_root}"
}
