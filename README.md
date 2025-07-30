import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

/// A reusable widget that displays an SVG icon inside a rounded card.
/// Shows an error fallback if the SVG fails to load.
class LogoCard extends StatelessWidget {
  /// Path to the SVG asset.
  final String svgAssetPath;

  /// Optional size of the card. Defaults to 60x60.
  final double size;

  const LogoCard({
    Key? key,
    required this.svgAssetPath,
    this.size = 60,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      width: size,
      height: size,
      padding: const EdgeInsets.all(10),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(12),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.05),
            blurRadius: 4,
            offset: const Offset(0, 2),
          ),
        ],
        border: Border.all(
          color: Colors.grey.shade300,
          width: 1,
        ),
      ),
      child: SvgPicture.asset(
        svgAssetPath,
        fit: BoxFit.contain,
        // Display a placeholder while loading
        placeholderBuilder: (context) => const Center(
          child: CircularProgressIndicator(strokeWidth: 2),
        ),
        // Fallback UI if SVG fails to load
        onPictureError: (exception, stackTrace) {
          debugPrint('Failed to load SVG: $exception');
        },
      ),
    );
  }
}