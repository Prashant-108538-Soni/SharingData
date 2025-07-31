import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

/// A reusable widget that displays an SVG icon inside a rounded card.
/// Shows an error fallback if the SVG fails to load.
class BillerImage extends StatelessWidget {
  /// Path to the SVG asset.
  final String svgPath;

  /// Optional size of the card. Defaults to 60x60.
  final double size;

  const BillerImage({
    super.key,
    required this.svgPath,
    this.size = 60,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      width: size,
      height: size,
      padding: const EdgeInsets.all(10),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(12),
        border: Border.all(
          color: Theme.of(context).primaryColor,
          width: 1,
        ),
      ),
      child: SvgPicture.asset(
        svgPath,
        fit: BoxFit.contain,
        // Add placeholderBuilder for error handling
        placeholderBuilder: (BuildContext context) =>
        const Icon(Icons.error_outline, color: Colors.red),
      ),
    );
  }
}
